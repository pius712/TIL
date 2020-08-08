# Multer AWS

Multer를 이용해서 AWS의 S3에 이미지 파일을 업로드 하는 과정에 대해서 살펴 볼 것이다.

AWS S3 버킷 생성 및 policy, access key 등은 Deployment/s3 문서에서 확인

## AWS SDK 
## install

### aws-sdk

Node.js에서 AWS SDK를 패키지를 다운 받아야 한다. 이 패키지에는 mazon S3, Amazon EC2, DynamoDB 및 Amazon SWF를 포함하는 AWS 서비스를 위한 JavaScript 객체가 제공된다.

즉, aws 접근 권한.

`npm i aws-sdk`

```
aws_access_key_id = your_access_key
aws_secret_access_key = your_secret_key
```

이를 .env에 저장한다
```
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
```
### multer-s3

`npm install --save multer-s3`

## 환경설정

SDK를 사용하기 전에 SDK 환경설정을 해줘야한다. 최소한 아래의 사항은 무조건 설정을 해줘야한다. 

- The`Region` in which you will request services.

- The `credentials` that authorize your access to SDK resources.

이 세팅에 permission에 대한 환경설정이 필요할 수 있다. 예를 들어서 S3 버킷에 대한 접근을 읽기 전용으로 제한할 수 있다. 

### Global Configuration

SDK 환경설정을 하는 방법은 두가지가 있다. 

- Set the global configuration using AWS.Config.

- Pass extra configuration information to a service object.

AWS.Config를 통한 Global configuration은 쉬운 방법이지만, 서비스 레벨의 configuration은 각각의 서비스를 더 많은 control 방법을 제공한다.  
AWS.Config는 default setting을 제공한다.  
하지만 각각의 service 객체에 configuration을 업데이트 할 수 있다. 

예를들어 아래와 같이 global configuration을 할 수 있다.

```js
var myCredentials = new AWS.CognitoIdentityCredentials({IdentityPoolId:'IDENTITY_POOL_ID'});
var myConfig = new AWS.Config({
  credentials: myCredentials, region: 'us-west-2'
});
```
또한, AWS.Config를 생선한 이후에 update 메서드를 통해서 업데이트를 할 수 있다. 

```js
myConfig = new AWS.Config();
myConfig.update({region: 'us-east-1'});
```

static getCredentials method를 통해서 default credentials를 가져올 수도 있다. 

```js
var AWS = require("aws-sdk");
AWS.config.getCredentials(function(err) {
  if (err) console.log(err.stack);
  // credentials not loaded
  else {
    console.log("Access key:", AWS.config.credentials.accessKeyId);
  }
});
```
Similarly, if you have set your region correctly in your config file, you get that value by setting the AWS_SDK_LOAD_CONFIG environment variable is set to a truthy value and calling the static region property of AWS.config:
```js
var AWS = require("aws-sdk");

console.log("Region: ", AWS.config.region);
```

## 실제 code

```js
//router/post.js
const AWS = require("aws-sdk");
const s3 = new AWS.s3();
const multerS3 = require("multer-s3");

const myConfig = new AWS.Config();
myConfig.update({
  region: "ap-northeast-2",
  accessKeyId: process.env.AWS_ACCESS_KEY_ID,
  secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
});
```

### Configure Your Credentials

```js
var AWS = require("aws-sdk");

AWS.config.getCredentials(function(err) {
  if (err) console.log(err.stack);
  // credentials not loaded
  else {
    console.log("Access key:", AWS.config.credentials.accessKeyId);
  }
});
```

```js
var AWS = require('aws-sdk');
var s3 = new AWS.S3();
// 버킷 이름은 모든 S3 사용자에게 고유한 것이어야 합니다.
var myBucket = 'my.unique.bucket.name';
var myKey = 'myBucketKey';
s3.createBucket({Bucket: myBucket}, function(err, data) {
if (err) {
   console.log(err);
   } else {
     params = {Bucket: myBucket, Key: myKey, Body: 'Hello!'};
     s3.putObject(params, function(err, data) {
         if (err) {
             console.log(err)
         } else {
             console.log("Successfully uploaded data to myBucket/myKey");
         }
      });
   }
});
```

## Multer S3

### Usage

`bucket`: The bucket used to store the file
`key` : The name of the file
`location` : The S3 url to access the file

```js
var aws = require('aws-sdk')
var express = require('express')
var multer = require('multer')
var multerS3 = require('multer-s3')
 
var app = express()
var s3 = new aws.S3({ /* ... */ })
 
var upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: 'some-bucket',
    metadata: function (req, file, cb) {
      cb(null, {fieldName: file.fieldname});
    },
    key: function (req, file, cb) {
      cb(null, Date.now().toString())
    }
  })
})
```


## code

### prev
```js 
// route/post/js

try {
  fs.accessSync("uploads");
} catch (error) {
  fs.mkdirSync("uploads");
}
const upload = multer({
  storage: multer.diskStorage({
    destination(req, file, cb) {
      cb(null, "uploads");
    },
    filename(req, file, cb) {
      const ext = path.extname(file.originalname);
      const basename = path.basename(file.originalname, ext);
      cb(null, basename + "_" + Date.now() + ext);
    },
  }),
  limits: {
    fileSize: 20 * 1024 * 1024,
  },
});

ter.post(
  "/images",
  upload.array("image", 5),
  isLoggedIn,
  async (req, res, next) => {
    console.log(req.files);
    res.json(req.files.map((file) => file.filename));
  }
);
```
### next

```js
const AWS = require("aws-sdk");
const s3 = new AWS.s3();
const multerS3 = require("multer-s3");
const router = express.Router();

const myConfig = new AWS.Config();
myConfig.update({
  region: "ap-northeast-2",
  accessKeyId: process.env.AWS_ACCESS_KEY_ID,
  secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
});

const upload = multer({
  storage: multerS3({
    s3: s3,
    bucket: "react-fittil",
    key: function (req, file, cb) {
      cb(null, `original/${Date.now()}_${path.basename(file.originalname)}`);
    },
  }),
  limits: {
    fileSize: 20 * 1024 * 1024,
  },
});

router.post(
  "/images",
  upload.array("image", 5),
  isLoggedIn,
  async (req, res, next) => {
    console.log(req.files);
    // res.json(req.files.map((file) => file.filename));
    // s3 변경 후
    res.json(req.files.map((file) => file.location));
  }
);
```

## front 코드에 영향?

backend router에서 
```js
res.json(req.files.map((file) => file.filename))
```
위와 같이 response를 해주었다. 
따라서, store에 imagePaths 배열에는 지금까지 file의 이름만 저장되었다. 

이를 front 화면에서 띄워주기 위해서, backend에서 
```js
// app.js
app.use("/", express.static(path.join(__dirname, "uploads")));
```
위와 같은 설정을 해주었다. 

front에서는 아래와 같은 방식(`${backUrl}/${image}`)으로 접근했는데, 이제, imagePaths로 보내주는 데이터가 S3의 image path이기 때문에 그냥 (`image`)만 해줘도 된다.
 
```js
// postform.js
const { imagePaths, addPostDone } = useSelector(state => state.post);
return(
  <div>
    {imagePaths.map((image, idx) => (
      <div key={image}>
        <PreviewImage src={`${backUrl}/${image}`} />
        <button onClick={() => onRemoveImage(idx)}>X</button>
      </div>
    ))}
  </div>
);
```