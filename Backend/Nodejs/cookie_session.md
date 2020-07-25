# Cookie & Session

## Cookie

### session cookie & permanent cookie

- session cookie
  휘발성 쿠키

- permanent cookie
  expire 지정해서 브라우저를 꺼도 살아있는 쿠키

### 옵션 Secure & http only

- secure
  javascript로 cookie를 접근 못하게 하는 것.

### 옵션 path & domain

- path
  `Path=/cookie` 처럼 옵션을 주면 해당 path와 그 하위 path에서만 cookie가 유효하다.

- domain

## cookie-parser

Cookie header를 파싱하여, `req.cookies`를 만들어 준다. req.cookies는 cookie의 이름을 key로 하는 객체이다.  
secret 문자열을 전달하여, signed cookie를 사용할 수도 있다. 

### install
`$ npm install cookie-parser`
`var cookieParser = require('cookie-parser')`

### API

`app.use(cookieParser(secret, options))`

cookie parser 미들웨어 함수를 만든 다음에 추가해준다. 

- `secret`: 문자열을 cookie를 sign하는데 사용한다. 명시하지 않으면, signed cookie를 parsing하지 않는다. 만약, 문자열을 인자로 넘기는 경우에, 이 문자열이 secret으로 사용된다. 배
- `options` an object that is passed to cookie.parse as the second option. See cookie for more information.
  - `decode` a function to decode the value of the cookie

request의 header 통해 들어오는 Cokie를 파싱하고, 이 쿠키를 `req.cookies`로 만들어준다.  
secret이 있는 경우에는 `req.signedCookies`로 만들어준다. 이 속성은 cookie name/cookie value의 쌍으로 이루어 져있다. 

When secret is provided, this module will unsign and validate any signed cookie values and move those name value pairs from req.cookies into req.signedCookies. A signed cookie is a cookie that has a value prefixed with s:. Signed cookies that fail signature validation will have the value false instead of the tampered value.

In addition, this module supports special “JSON cookies”. These are cookie where the value is prefixed with j:. When these values are encountered, the value will be exposed as the result of JSON.parse. If parsing fails, the original value will remain.

## epxress-session 

쿠키를 통해서만 인증을 구현하면 브라우저에 그대로 노출되기 때문에, 위험하다.

### install
`$ npm install express-session`
`var session = require('express-session')`

### API


```js
app.use(
  session({
    secret: 'asadlfkj!@#!@#dfgasdg', // required option
    resave: false,
    saveUninitialized: true,
  }),
);
app.get('/', function(req, res, next) {
  console.log(req.session); 
  // 미들웨어를 추가해주면, 
  // request 객체에 session 이라는 객체를 추가해준다.
  if (req.session.num === undefined) {
    req.session.num = 1;
  } else {
    req.session.num = req.session.num + 1;
  }
  res.send(`Views : ${req.session.num}`);
});
```
- secret – 쿠키를 임의로 변조하는것을 방지하기 위한 값 입니다. 이 값을 통하여 세션을 암호화 하여 저장합니다.
- resave – 세션을 언제나 저장할 지 (변경되지 않아도) 정하는 값입니다. express-session documentation에서는 이 값을 false 로 하는것을 권장하고 필요에 따라 true로 설정합니다.
- saveUninitialized – 세션이 저장되기 전에 uninitialized 상태로 미리 만들어서 저장합니다.
```js
// routes/user.js

// email이랑 password 검사
await User.findOne();
// 세션에 저장
user[cookie] = 유저정보;
//프론트에 쿠키 내려보내주기
```
