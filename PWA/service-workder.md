# Service Workder

- Caching
- Offline
- Native feature

## 특징

chrome://serviceworker-internals

- 브라우저의 백그라운드에서 실행된다. 웹페이지와 별개의 라이프 사이클
  - UI쓰레드와는 별도로 돌아간다.
- 캐쉬 제공 및 서버에 자원 요청
  - 프로그래밍 가능한 프록시
- 브라우저에 종속적인 생명주기로 백그라운드 동기화 기능 제공

- 웹과 모바일 Push 수신이 가능하도록 Notification 제공
- navigator.serviceworker로 접근
- 기존 js와 스코프가 다르다.
- DOM에 접근 불가
- 사용 x -> 종료, 필요시 동작(이벤트 기반)
