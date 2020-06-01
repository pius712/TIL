# HTTP

HTTP는 HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는  클라이언트-서버 프로토콜이다. 

## Client

대게는 사용자의 브라우저가 client이다. 요청을 보내는 개체이다. 

## Web Server

Client의 요청에 대한 Response를 해준다. 

## Request

```
GET / HTTP/1.1  // 메서드 | 경로 | 프로토콜 버전
HOST: developer.mozilla.org // 헤더
Accept-Language: kr
```
- HTTP 메서드, 보통 클라이언트가 수행하고자 하는 동작을 정의한 GET, POST 같은 동사나 OPTIONS나 HEAD와 같은 명사입니다. 일반적으로, 클라이언트는 리소스를 가져오거나(GET을 사용하여) HTML 폼의 데이터를 전송(POST를 사용하여)하려고 하지만, 다른 경우에는 다른 동작이 요구될 수도 있습니다.
- 가져오려는 리소스의 경로; 예를 들면 프로토콜 (http://), 도메인 (여기서는 developer.mozilla.org), 또는 TCP 포트 (여기서는 80)인 요소들을 제거한 리소스의 URL입니다.
- HTTP 프로토콜의 버전.
- 서버에 대한 추가 정보를 전달하는 선택적 헤더들.
- POST와 같은 몇 가지 메서드를 위한, 전송된 리소스를 포함하는 응답의 본문과 유사한 본문.

## Response


```
HTTP/1.1 200 OK  
// 프로토콜 버전 | status code | status msg
Date : ...  // 헤더
Server : ...
Last-Modified : ...
Content-Length : ...
Content-Type : ...
```

- HTTP 프로토콜의 버전.
- 요청의 성공 여부와, 그 이유를 나타내는 상태 코드.
- 상태 코드의 짧은 설명을 나타내는 상태 메시지.
- 요청 헤더와 비슷한, HTTP 헤더들.
- 선택 사항으로, 가져온 리소스가 포함되는 본문.