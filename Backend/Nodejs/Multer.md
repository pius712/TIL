# Multer

Multer는 파일 업로드를 위해 사용되는 multipart/form-data 를 다루기 위한 node.js 의 미들웨어 입니다. 효율성을 최대화 하기 위해 busboy 를 기반으로 하고 있습니다.

주: Multer는 multipart (multipart/form-data)가 아닌 폼에서는 동작하지 않습니다.

## install

`$ npm install --save multer`

## Usage

Multer는 request 객체에 body 객체와 file, files 객체를 추가해준다. `req.body` `req.file` `req.files`
`req.body` 객체에는 form 태그의 text 필드의 값들을 포함하고 있다.  
그리고 `req.file` `req.files` 객체에는 form에 의해서 업로드 된 files를 가지고 있다.
즉, middle ware로 넘겨주는 `upload`가 front에서 올려주는 이미지 파일에 대해서 로직을 실행해주고,  
위의 객체에 해당 정보들을 넘겨준다. `(req,res,next)=>{}` 내에서 처리된 정보들을 다룰 수 있다.  

기본적인 예시:

form태그에 `enctype="multipart/form-data"` 설정을 꼭 해야한다. 

```html
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="avatar" />
</form>
```

```js
var express = require('express')
var multer  = require('multer')
var upload = multer({ dest: 'uploads/' })

var app = express()

app.post('/profile', upload.single('avatar'), function (req, res, next) {
  // req.file is the `avatar` file
  // req.body will hold the text fields, if there were any
})

app.post('/photos/upload', upload.array('photos', 12), function (req, res, next) {
  // req.files is array of `photos` files
  // req.body will contain the text fields, if there were any
})

var cpUpload = upload.fields([{ name: 'avatar', maxCount: 1 }, { name: 'gallery', maxCount: 8 }])
app.post('/cool-profile', cpUpload, function (req, res, next) {
  // req.files는 객체이고 fieldname은 그 객체의 key이고, 그 값은 파일 객체이다. 
	// req.files is an object (String -> Array) where fieldname is the key, and the value is array of files
  // e.g.
  //  req.files.avatar[0] -> File
  //  req.files.gallery -> Array
  // req.body will contain the text fields, if there were any
})
```
예시 코드

Take special note of the enctype="multipart/form-data" and name="uploaded_file" fields:

```html
<form action="/stats" enctype="multipart/form-data" method="post">
  <div class="form-group">
    <input type="file" class="form-control-file" name="uploaded_file">
    <input type="text" class="form-control" placeholder="Number of speakers" name="nspeakers">
    <input type="submit" value="Get me the stats!" class="btn btn-default">            
  </div>
</form>
```
js file에는 file과 body 모두에 접근 하기 위해서 아래의 라인을 추가해야한다.  
form 태그의 name field의 값을 `upload` 함수에 사용된다는 것을 주목.  
이 name field의 값이 multer에게 request에서 어떤 field를 찾아야하는지 알려준다.  
HTML의 form과 server에서 이 값이 일치하지 않으면 upload는 실패한다. 

```js
var multer  = require('multer')
var upload = multer({ dest: './public/data/uploads/' })
app.post('/stats', upload.single('uploaded_file'), function (req, res) {
   // req.file is the name of your file in the form above, here 'uploaded_file'
   // req.body will hold the text fields, if there were any 
   console.log(req.file, req.body)
});
```
## back

```js
// app.js
app.use('/', express.static('uploads'));
```

```js
// routes/post
const upload = multer({
	storage: multer.diskStorage({
		destination(req, file, done) {
			done(null, 'uploads');
		},
		filename(req, file, done) {
			const ext = path.extname(file.originalname);
			// 확장자를 뽑아오는 것.
			const basename = path.basename(file.originalname, ext);
			// pius.png, basename = pius, ext = .png
			done(null, basename + Date.now() + ext);
		},
	}),
	limit: { fileSize: 20 * 1024 * 1024 },
	// 사이즈 제한
});
```

여기서 `upload.array('image')`는 req.files로 들어오는 것이 'image' array여야 한다는 뜻.

```js
router.post('/images', isLoggedIn, upload.array('image'), (req, res) => {
	// console.log(req.files);
	res.json(req.files.map(v => v.filename));
});

upload.single; //파일 하나
upload.array; // 같은 키로 여러개
upload.fields; // 다른 키로 여러개 ?
```

알아서 storage에 저장을 해주고, req.files에 배열 형태로 파일을 저장해준다.

## front

### React 


### Vue

```js
onChangeImages(e) {
  console.log(e.target.files);
  const imageFormData = new FormData();
  [].forEach.call(e.target.files, f => {
    // e.target.files가 유사배열이라서, forEach를 못쓴다. forEach는 인자가 콜백함수.
    imageFormData.append('image', f); //{ image: [file1, file2] }
  });
  this.$store.dispatch('posts/uploadImages', imageFormData);
},
```

```js
//store/post
actions = {
  uploadImages({ commit }, payload) {
    this.$axios
      .post('http://localhost:8080/post/images', payload, {
        withCredentials: true,
      })
      .then(res => {
        console.log('uploaded');
        commit('concatImagePaths', res.data);
      })
      .catch(() => {});
  }
},
```

```js
mutations = {
	concatImagePaths(state, payload) {
		state.imagePaths = state.imagePaths.concat(payload);
	},
	removeImagePath(state, payload) {
		state.imagePaths.splice(payload, 1);
	},
};
```

```html
<div v-for="(p, i) in imagePaths" :key="i" style="display:inline-block">
	<img :src="`http://localhost:8080/${p}`" style="width: 200px" />
	<div>
		<button type="button" @click="onRemoveImage(i)">
			제거
		</button>
	</div>
</div>
<!-- PostFrom.vue -->
computed: { ...mapState('posts', ['imagePaths']), },
```

