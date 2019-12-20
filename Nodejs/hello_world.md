# hello_world


```javascript 
const http = require('http');

const hostname = '127.0.0.1';

const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

cf) 템플릿 문자열  \`http://${hostnmae}:${port} \` 이런 식으로 백틱으로 감싸고 내부에 ${} 를 통해서 변수를 표현할 수 있다. 


 ~ curl -X GET 'localhost:3000/users'

```bash
~ node-tuto node helloworld.js
Server running at http://127.0.0.1:3000/
'/users'
``` 