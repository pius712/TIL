# HTTP

## HTTP 메시지

### 메서드 

* GET
* POST
* PATCH
* PUT
* DELETE

웹 클라이언트에서 HTML form을 통해 서버로 데이터를 보낸다. 이 form에는 2가지 중요한 속성이 `action`과 `method`이다. 

get 방식 (html / http request)

```html
<form action="http://foo.com" method="get">
  <input name="say" value="Hi">
  <input name="to" value="Mom">
  <button>Send my greetings</button>
</form>
```

```bash
GET /?say=Hi&to=Mom HTTP/1.1
Host: foo.com
```

post 방식 (html / http request)

```html
<form action="http://foo.com" method="post">
  <input name="say" value="Hi">
  <input name="to" value="Mom">
  <button>Send my greetings</button>
</form>
```  

```bash
POST / HTTP/1.1
Host: foo.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 13

say=Hi&to=Mom
```