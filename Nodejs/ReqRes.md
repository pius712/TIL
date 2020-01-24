# Request & Response

## Request 객체

- 클라이언트 요청 정보를 담은 객체를 요청(Request)객체라고 한다.
- express의 요청 객체는 http 모듈의 request 객체를 래핑한 것이다.
- req.params(), req.query(), req.body(), req.json() 메소드를 주로 사용한다.

```javascript
const http = require('http');
const server = http.createServer((req, res) => {});
```

위에서 createSever() 함수의 인자 `req` `res`는 객체이다.

### req.body

키-벨류 쌍의 데이터를 포함한다. `express.json()` or `express.urlencoded()` 와 같은 body-parsing middle ware를 사용하면 값이 채워진다.

```js
var express = require('express');

var app = express();

app.use(express.json()); // for parsing application/json
app.use(express.urlencoded({ extended: false })); // for parsing application/x-www-form-urlencoded

app.post('/profile', function(req, res, next) {
  console.log(req.body);
  res.json(req.body);
});
```

JSON의 형태로 front에서 값을 보낸다면, node에서 이를 req.body에 파싱하여 보내준다.
URL-encoded 형식으로 name=pius&page=3 과 같은 형식으로 보내면, req.body에 {name: 'pius', page: '3'}으로 만들어준다.

### req.params

라우트의 파라미터 객체와 맵핑되는 프로퍼티이다. `/user/:name` 와 같은 라우트가 있을 때, `req.params.name`이 사용가능하다.

```js
// GET /user/tj
console.dir(req.params.name);
// => 'tj'
```

### req.query

라우트에 있는 쿼리 스트링 파라미터를 가지는 객체이다. 쿼리 스트링이 없으면 빈 객체.

기본적으로, req.query는 사용자에 의해 컨트롤 되는 input 기반의 정보이기 때문에 이를 쓰기 위해서는 validation이 필요하다.  
예를들어, GET /shoes?color[]=blue&color[]=black&color[]=red 이런식으로 들어올 수 도 있기 때문에, 함부러 toString()과 같은 함수를 사용해서는 안된다.

```js
// GET /search?q=tobi+ferret
console.dir(req.query.q);
// => 'tobi ferret'

// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
console.dir(req.query.order);
// => 'desc'

console.dir(req.query.shoe.color);
// => 'blue'

console.dir(req.query.shoe.type);
// => 'converse'
```

## Response 객체

### `res.app`

이 속성은 해당 미들웨어를 사용하고 있는 Express application의 인스턴스를 참조한다. 참고로 `res.app === req.app`  
 라우터 디렉토리의 라우터 파일에서는 app인스턴스가 없기 때문에, app.get()을 할 수 없다. 그렇기 때문에 그 경우에는 res.app과 같은 방식을 통해서 app 객체에 접근한다.

### `res.locals`

서버에 접속하는 request/ response 한 사이클 동안에 존재하는 reponse의 지역 변수이다. 그러한 점을 제외하고는 `app.locals`와 같은데...  
`app.locals`는 app 인스턴스의 변수로 일종의 전역변수이고, request/ respons의 사이클과는 관계없이 항상 똑같다.  
즉, 아래의 코드와 같이 reqeust를 통에 user의 아이디를 알았다고 했을때 res.locals.user 와 .authenticated는 그 사이클 동안에만 유지가 되고, 그 이전에 app.set('view engine', 'pug')와 같은 설정은 그대로 다른 사이클에도 계속 존재하는 것이다.

```javascript
app.use(function(req, res, next) {
  res.locals.user = req.user;
  res.locals.authenticated = !req.user.anonymous;
  next();
});
```

### res.json()

JSON 응답을 보낸다. 안에 json을 넣으면, json.stringify()를 호출해서 response로 보내준다.

파라미터는 어떠한 JSON type이 될 수 있는데,
The parameter can be any JSON type, including object, array, string, Boolean, number, or null, and you can also use it to convert other values to JSON.

res.json(null)
res.json({ user: 'tobi' })
res.status(500).json({ error: 'message' })

router.get('/', function(req, res, next) {
// res.send('respond with a resource');
User.findAll()
.then(users => {
res.json(users);
})
.catch(err => {
console.error(err);
next(err);
});
});
