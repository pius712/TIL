# Crypt

회원가입시에, post 요청을 보내도 이 정보는 노출된다. (network tap을 통해서 확인 가능하다)

그래서 패스워드 암호화를 한다.

1. bcrypt
2. scrypt
3. pbkdf2

## bcrypt

```js
const bcrypt = require('bcrypt');
app.post('/', async (req, res, next) => {
  try {
    // console.log(req.body);
    const hash = bcrypt.hash(req.password, 12);
    const newUser = await User.create({
      email: req.body.email,
      password: hash,
      nickname: req.body.nickname,
    });
    res.status(201).json(newUser);
    //newUser은 Model인데, 이 Model은 js 객체의 인스턴스이다. 따라서 json()함수를 사용해서 json으로 만들 수 있다.
  } catch (err) {
    console.error(err);
    next(err);
  }
});
```
