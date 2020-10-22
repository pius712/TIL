# VScode

## shortcut

### 한 줄 삭제

- command + shift + K

### 단어 선택

- ctrl + shift + 방향키

방향키를 누를때마다 선택되는 영역이 커진다.

### 줄 위 아래

- option + 방향키 (위/아래)

### 한 라인 복사후 아래에 붙여넣기

- command + shift + 방향키 아래/위

### 블럭 처음/끝 이동

- command + shift + \

### 리팩토링

- F2

F2를 누르면 함수 선언부/호출부의 이름이 모두 바뀐다.
다만, 이 함수를 destructring 하는 부분은 아래와 같이 바뀐다.

```js
// 바뀌기 전
class foo {
  function before () {

  }

  function func() {
    const { before } = this;
    before();
  }
}
// 바뀐 후
class foo {
  function after () {

  }
  function func() {
    const { after: before } = this;
    before();
  }
}
```

### 호출부에서 정의로

다른 파일에 import하는 것도 된다고 하는데 잘 안된다.

- F12

### 정의에서 모든 호출부

- option + shift + F12

### 커서 이동 (탐색기 <-> 코드 에디터 <-> 터미널)

- command + 0 : 탐색기로 이동(vscode 왼편)
- command + 1 : 코드 부분으로 커서 이동
- ctrl + `(백틱) : 터미널 부분으로 커서 이동

### 탭(코드 윗부분) 이동

- ctrl + option + 키보드 좌우 : 좌우 이동

### 명령어 검색

- F1

### 바로가기(shortcut) 검색

- command + k + s

### 파일 바로가기

- command + p

### Symbol로 찾기

- command + t

함수선언, 클래스 이름 등의 심볼을 검색(탭에 올라온 것들 중에서 찾음)

## Extension

### Bookmarks

특정 라인에 북마크해서 코드 리뷰 혹은 리딩할 때, 유용해보입니다.

settings.json 파일에서 `"bookmarks.navigateThroughAllFiles": true,` 설정하면 모든 파일에서 점프 가능

- option + command + k : 북마크 설정
- option + command + j : 이전 북마크 이동
- option + command + l : 다음 북마크 이동
