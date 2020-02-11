# dotenv

소스코드에 비밀번호와 같은 설정과 관련된 내용들을 넣으면 보안에 취약해진다.

```bash
npm i dotenv
```

.env 파일은 키 = 쌍 형식으로 저장한다.

```JSON
// .env
COOKIE_SECRET = secret
```

```js
//app.js
require('dotenv').config();
```

위와 같이 설정을 해주면 process.env.키 에 값이 들어가게 된다. 즉, `process.env.COOKIE_SECRET`에 secret이라는 value가 들어가게 된다.
