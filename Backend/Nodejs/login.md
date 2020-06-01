# Login

## 로그인이란?

서버에서 세션을 사용자 정보(권한, 이전 게시글 등...)
세션을 통해 권한, 정보를 알아내고 처리할 수 있게 해줌.

## 로직

1. 아이디와 비밀번호를 입력
2. 인증
3. 서버에서 쿠키를 심어준다.
4. 서버에 요청시에 http 헤더로 쿠키를 보내준다.
5. 세션에서 확인

```js
// routes/user.js

// email이랑 password 검사
await User.findOne();
// 세션에 저장
user[cookie] = 유저정보;
//프론트에 쿠키 내려보내주기
```

패키지

- passport
- passport-local
- passport-kakao
- etc...

## passport

### 설정(app.js)

```js
//app.js
const passport = require('passport');
const session = require('express-session');
const cookie = require('cookie-parser');

const passportConfig = require('./passport');
const app = express();

app.use(cookie('cookiesecret'));
// session을 사용하려면 쿠키도 필요함.
app.use(
  session({
    resave: false,
    saveUninitialized: false,
    secret: 'cookiesecret',
  }), // passport의 세션을 사용하려면 session을 설치해줘야함
);
app.use(passport.initialize());
// passport init. req.login(), req.logout() 만들어준다.
app.use(passport.session());
// login session을 사용
```

### Session

일반적인 웹 앱은, 유저의 정보를 login request에서 확인한 뒤에는 그 정보를 계속 가지고 있지 않는다. 인증이 성공하면, 서버는 session을 만들어 가지고 있고, 클라이언트(유저의 브라우저)는 쿠키를 저장해서 가지고 있는다.

이후의 request는 유저의 개인정보가 없고, session을 확인할 수 있는 유일한 쿠키를 가지고 있다. 로그인 세션을 지원하기 위해서, passport는 유저의 인스턴스를 세션으로/세션으로부터 serialize와 deserialize 할 수 있는 함수를 제공해준다.

```js
passport.serializeUser(function(user, done) {
  //req.login의 user 인자가 여기로 들어온다.
  done(null, user.id);
});

passport.deserializeUser(function(id, done) {
  User.findOne({
      where: {
        email: id,
      },
    })
      .then(user => {
        done(null, user);
      })
      .catch(err => {
        console.error(err);
        return done(err);
      });
  });
});
```

위의 코드는 user.id 만 session으로 serialize 되었다.  
(deserializeUser 부분)이후의 request를 받을 때, 이 id는 유저를 찾을 때 사용된다. 그리고 데이터 베이스를 통해 회원의 정보를 찾은 후, `done()`을 호출하여, req.user에 user의 정보를 저장한다. (+ req.authenticated() === true 가 된다.)

The serialization and deserialization logic is supplied by the application, allowing the application to choose an appropriate database and/or object mapper, without imposition by the authentication layer.

### request 인증하기(Authenticating requests)

기본적으로 passport를 통해 계정을 인증하는 메서드는 `passport.authenticate()`이다.  
첫번째 인자로는 strategy가 오게 된다.
두번째 인자에는 객체를 통해 options 설정할 수 있고, custom callback 함수를 만들 수도 있다.  
메서드 자체만으로 미들웨어로 사용이 가능하나, req,res 객체를 이용하기 위해서 route handler 미들웨어 함수 내에서 실행하기도 한다.

```js
1. 미들웨어로 사용

app.post('/login',
  passport.authenticate('local'),
  function(req, res) {
    // If this function gets called, authentication was successful.
    // `req.user` contains the authenticated user.
    res.redirect('/users/' + req.user.username);
  });
2. route handler에서 사용.

app.get('/login', function(req, res, next) {
  passport.authenticate('local', function(err, user, info) {
    if (err) { return next(err); }
    if (!user) { return res.redirect('/login'); }
    req.logIn(user, function(err) {
    if (err) { return next(err); }
    return res.redirect('/users/' + user.username);
    });
})(req, res, next);
// 이렇게 쓰는 이유에 대해서는 음.. passport.authenticate()가 미들웨어로 쓰였다. 즉, 저 함수 호출의 리턴 값이 함수라는 뜻. 그렇기 때문에, 다른 미들웨어 내에서 "호출" 하기 위해서는 ()를 붙여서 호출해야하는데, 미들웨어의 인자는 req,res,next 이므로 (req,res,next)를 붙여서 호출한다.
});
```

성공시, req.login() 호출 -> req.user(session)에 저장.  
// 어떻게 저장? --> 위 session part

```js
routes / user;
app.post('/user/login', (req, res) => {
  passport.authenticate('local', (err, user, info) => {
    // local strategy(passport.local.js의 passport.use() 함수) 실행 --> return done() 이게 뒤에 콜백 인자로 들어온다.
    if (err) {
      console.error(err);
      return next(err);
    }
    if (info) {
      return res.status(401).send(info.reason);
    }
    return req.login(user, async err => {
      //세션에다 사용자 정보 저장 ( how? sereilizeUser )
      if (err) {
        console.error(err);
        return next(err);
      }
      return res.json(user);
      // respond를 안해주면, authenticate() 함수가 실패한 것으로 인식한다. 그러므로 바깥에 하지말고 안에 하도록.
    }); // req.login ?! --> 원래 있는게 아니라 passport.initialize()을 하면 req.login/ req.logout 추가해준다.
  })(req, res, next);
}); //authenticate(strategy, options)
```

## Strategy

`passport.authenticate()` 첫번째 인자에, strategy를 입력하면, 그 작업을 strategy에게 위임한다. 아래는 Strategy의 예시 코드이다.

`passport.use()`의 첫번째 인자는 일종의 옵션인데, 원래는 인증을 하는 form 태그의 이름을 `name`, `password`로 맞춰줘야하는데 이를 사용자화 할 수 있다.

```html
<form action="/login" method="post">
  <input type="text" name="username" />
  <input type="password" name="password" />
</form>
```

// form data가 post 될 때, 그 input의 reference는 name attribute로 한다.
// form이 method=get 일때는 body는 비어있고 url에 포함되고, post일때는 url에는 비어있고, bodt에 key=value 형식으로 들어있다.

```js
//passport.local.js
const passport = require('passport');
const bcrypt = require('bcrypt');
const db = require('../models');
const { Strategy: LocalStrategy } = require('passport-local');
// 비구조화 할당인데, Strategy를 LocalStrategy라는 이름으로 가지고 온다.
module.exports = () => {
  passport.use(
    new LocalStrategy(
      {
        usernameField: 'email', //req.body.email
        passwordField: 'password', // req.body.password
      },
      // 참고
      // JSON의 형태로 front에서 값을 보낸다면, node에서 이를 req.body에 파싱하여 보내준다.
      // URL-encoded 형식으로 name=pius&page=3 과 같은 형식으로 보내면, req.body에 {name: 'pius', page: '3'}으로 만들어준다.
      // form 데이터를 post 하면, req.body객체에 그 값이 담기게 된다.
      //
      async (email, password, done) => {
        try {
          const exUser = await db.User.findOne({ where: { email } });
          if (!exUser) {
            return done(null, false, { reson: '존재하지 않는 사용자입니다' });
            // done(에러, 성공, 실패);
          }
          const result = await bcrypt.compare(password, exUser.password);
          if (result) {
            return done(null, exUser);
          } else {
            return done(null, false, { reson: '비밀번호가 틀립니다.' });
          }
        } catch (err) {
          console.error(err);
          return done(err);
        }
      },
    ),
  );
};
```
