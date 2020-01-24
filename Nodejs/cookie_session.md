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

## Session

쿠키를 통해서만 인증을 구현하면 브라우저에 그대로 노출되기 때문에, 위험하다.

```js
app.use(
  session({
    secret: 'asadlfkj!@#!@#dfgasdg', // required option
    resave: false,
    saveUninitialized: true,
  }),
);
app.get('/', function(req, res, next) {
  console.log(req.session); // request 객체에 session 이라는 객체를 추가해준다.
  if (req.session.num === undefined) {
    req.session.num = 1;
  } else {
    req.session.num = req.session.num + 1;
  }
  res.send(`Views : ${req.session.num}`);
});
```

```js
// routes/user.js

// email이랑 password 검사
await User.findOne();
// 세션에 저장
user[cookie] = 유저정보;
//프론트에 쿠키 내려보내주기
```
