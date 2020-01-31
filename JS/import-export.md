# import/export

```js
//bus.js
export const bus = new Vue();
// App.vue
import { bus } from './bus.js;

//bus.js
export default new Vue();
//App.js
import bus from './bus.js';
```

## Node

nodejs 환경에서는 조금 다르게 사용된다.  
exports가 하나의 객체이고 그 안에 속성으로 넣어줄 수 있다. 그러면 이는 destructuring을 해서 받을 수 있다.  
또는 module.exports = 객체 형식을 통해서도 가능하다. module.exports가 더 우선권을 가진다.

```js
// routes/ middleware.js
exports.isLoggedIn = (req, res, next) => {
  if (req.isAuthenticated()) {
    return next();
  }
  return res.status(401).send('로그인이 필요합니다.');
};

exports.isNotLoggedIn = (req, res, next) => {
  if (!req.isAuthenticated()) {
    return next();
  }
  return status(401).send('로그인한 사람은 접근할 수 없습니다.');
};
// 아래와 같은 방식으로 선언해도 된다.
// module.exports = {
//     isLoggedIn : (req,res,next) =>{},
//     isNotLoggedIn : (req,res,next) => {}
// }

// routes/index
const express = require('express');
const router = express.Router();
const { isLoggedInt, isNotLoggedIn } = require('./middleware');

router.get(/*...*/);

module.exports = router;
```
