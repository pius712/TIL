# module

* 내장 객체
  * global 
  * console 
* 내장 모듈
  * os
  * path
  * url
  * querystring
  * fs

## module system이란? 

```javascript
//var.js
const odd = 'odd';
const even = 'even';

module.exports = {
    odd,
    even,
};
// exports.odd = odd;
// exports.even = even;
//  exports에 객체를 담는 것이라서 위와 같이 가능. 

//func.js
const { odd, even } = require('./var');

function foo(){
    console.log('hello world');
}
module.exports = foo;

//index.js 
const { odd, even } = require('./var');  
const bar = require('./func');
// 비구조화 할당의 경우에는 변수의 이름이 같은 것과 매칭이 된다. 그 반면 그냥 하나의 값만 module.exports 했을 경우에는 이 것을 다른 이름의 변수로 받아도 받아진다. 즉 odd, even 순서가 바뀌어도 상관이 없이 같은 이름끼리 매칭이 된다. 
console.log(odd, even);
console.log(bar());
```
___

## 내장 객체 

### global 객체

```javascript
//globalA.js
module.exports = ()=> global.message;

// globalB.js
const A = require('./globalA');

global.message = '안녕하세요'
console.log(A());

```

### console 객체 

```javascript
const obj = {
    outer:{
        inner:{
            a:1,
        }
    }
}
console.time('checkTime');
// 이 사이의 시간을 측정할 수 있다. 
console.timeEnd('checkTime');

console.log('일반적인 로그');
console.dir(obj, { colors: true, depth:2 }); // 뒤에는 options

```

### __filename, __dirname

```javascript
//index.js
console.log(__filename);
console.log(__dirname);
```

```bash
>>> node index
/Users/pius/Documents/node-tuto/module/index.js
/Users/pius/Documents/node-tuto/module
```

___

## 내장 모듈

설치하지 않아도 사용할 수 있는 내장 모듈. 

### os 모듈

```javascript
const os = require('os');
console.log(os); 
```

위를 통해 확인해서 사용할 수 있다. 데스크탑 프로그램을 만들때 사용한다고 한다.

### path 모듈 

```javascript
const path = require('path');

path.sep  // 경로의 구분자입니다
path.delimiter //   
path.dirname(경로): 파일이 위치한 폴더 경로를 보여줍니다.
path.extname(경로): 파일의 확장자를 보여줍니다.
path.basename(경로, 확장자): 파일의 이름(확장자 포함)을 보여줍니다. 파일의 이름만 표시하고 싶다면 basename의 두 번째 인자로 파일의 확장자를 넣어주면 됩니다.

path.parse(경로) //파일 경로를 root, dir, base, ext, name으로 분리합니다.
path.format(객체) //path.parse()한 객체를 파일 경로로 합칩니다.

path.normalize(경로) //  /나 \를 실수로 여러 번 사용했거나 혼용했을 때 정상적인 경로로 변환해줍니다.

path.isAbsolute(경로) //파일의 경로가 절대경로인지 상대경로인지 true나 false로 알려줍니다.

path.relative(기준경로, 비교경로)// 경로를 두 개 넣으면 첫 번째 경로에서 두 번째 경로로 가는 방법을 알려줍니다.
```

중요한 메서드 

```javascript
path.join(경로, ...)
// 여러 인자를 넣으면 하나의 경로로 합쳐줍니다. 상대경로인 ..(부모 디렉터리)과 .(현 위치)도 알아서 처리해줍니다.

path.resolve(경로, ...)
// path.join()과 비슷하지만 차이가 있습니다. 차이점은 다음에 나오는 Note에서 설명합니다.
```

### url 모듈

```javascript
const url = require('url');

const URL = url.URL;
const myURL = new URL('https://github.com/pius712/TIL/blob/master/Nodejs/nodejs.md');
// 새로운 주소 체계 
console.log('new URL():', myURL);
console.log('url.format():',url.format(myURL));
console.log('---------------------------');
const parsedURL = url.parse('https://github.com/pius712/TIL/blob/master/Nodejs/nodejs.md'); 
// 기존의 주소 체계 
console.log('url.parse():', parsedURL);
```

parse() vs new URL()

parse()

```bash
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'github.com',
  port: null,
  hostname: 'github.com',
  hash: null,
  search: null,
  query: null,
  pathname: '/pius712/TIL/blob/master/Nodejs/nodejs.md',
  path: '/pius712/TIL/blob/master/Nodejs/nodejs.md',
  href: 'https://github.com/pius712/TIL/blob/master/Nodejs/nodejs.md'
}
```

new URL()

```bash
URL{
  href: 'https://github.com/pius712/TIL/blob/master/Nodejs/nodejs.md',
  origin: 'https://github.com',
  protocol: 'https:',
  username: '',
  password: '',
  host: 'github.com',
  hostname: 'github.com',
  port: '',
  pathname: '/pius712/TIL/blob/master/Nodejs/nodejs.md',
  search: '',
  searchParams: URLSearchParams {},
  hash: ''
}
```

## querystring 

```javascript
const url = require('url');
const quertystring = require('querystring');

const parsedUrl = url.parse('https://github.com/pius712/TIL/blob/master/Nodejs/nodejs.md');
const query = querystring.parse(parsedUrl.query);

console.log('querystring.parse():', query);
console.log('querystring.stringify():', querystring.stringify(query));
```

예를 들어 `'foo=bar&abc=xyz&abc=123'` 와 같은 query string이 있을때,

```javascript
querystring.parse(query)
```

코드를 호출하면, 아래와 같이 객체의 형태가 된다.

```javascript
{
  foo: 'bar',
  abc: ['xyz', '123']
}
```

### util

1. deprecate

```javascript
const util = require('util');

const dontuseme = util.deprecate((x.,y)=>{
  console.log(x+y);
}, 'message');

dontuseme(1,2);
```

```bash
3
(node:5347) DeprecationWarning: message
```

api 만들 때, 사용하는 그런 메서드인듯. 

2. promisify

```javascript
const util = require('util');
const crypto = require('cryto');

const dontuseme = util.deprecate((x, y)=>{
  console.log(x+y);
}, 'message');

dontuseme(1,2);

const randomBytesPromise = util.promisify(crypto.randomBytes);
const pbkdf2Promise = util.promisify(crypto.pbkdf2);

crypto.randomBytes(64, (err,buf)=>{
  const salt = buf.toString('base64');
  console.log('salt', salt);
  console.time('암호화');
  crypto.pbkdf2('pius', salt, 651395, 64, 'sha512', (err,key)=>{
    console.log('password', key.toString('base64'));
    console.timeEnd('암호화');
  });
});
crypto.randomBytes(64);

randomBytesPromise(64)
  .then((buf)=>{
    const salt = buf.toString('base64');
    console.log('salt', salt);
    console.time('암호화');
    return pbkdf2Promise('pius', salt, 651395, 64, 'sha512');
  })
  .then((key)=> {
    console.log('password', key.toString('base64'));
  })
  .catch((err)=>{
    console.error(err);
  })
(async ()=>{
  const buf = await randomBytesPromise(64);
  const salt = buf.toString('base64');
  const key = await pbkdf2Promise('pius', salt, 651395, 64, 'sha512');
  console.log('password', key.toString('base64'));
  
})();
```

### fs 모듈

```javascript
const fs = require('fs');
fs.readFile('경로', (err,data)=>{
  if(err){
    throw err;
  }else{
    console.log(data);
  }
})
```

### event 모듈

이벤트 리스너를 생성하고, 특정 이벤트가 발생할 경우 로직을 실행.

```javascript
const EventEmitter = require('events');

const myEvent = new EventEmitter();

myEvent.addListener('visit',()=>{
    console.log('thank you for visit');
});

myEvent.on('end', ()=>{
    console.log('get out of here');
});

myEvent.on('end',()=>{
    console.log('fuck off');
});

myEvent.once('special', ()=>{
    console.log('한 번 실행됨');
});

myEvent.emit('visit');
myEvent.emit('end');
myEvent.emit('special');
myEvent.emit('special');

myEvent.on('continue', ()=>{
    console.log('listening...');
});

myEvent.removeAllListeners('continue');
myEvent.emit('continue');

const callback1 = ()=>{
    console.log('callback1');
}
const callback2 = ()=>{
    console.log('callback2');
}
myEvent.on('end1', callback1);
myEvent.on('end1', callback2);
myEvent.removeListener('end1', callback1);
myEvent.emit('end1');
```

```bash
thank you for visit
get out of here
fuck off
한 번 실행됨
callback2
```