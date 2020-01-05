# Git

## 동작 원리

작업 트리 -> 스테이지 -> 저장소
## CLI

### 환경설정 

```git
git config --global user.name "pius712"
git config --global user.email "aksfbsgnlfls@gmail.com"
```

### 초기화

```bash
git init
```

### 수정한 파일 스테이징

수정한 파일을 스테이지로 올리는 것

```bash
// 모든 파일
git add .
// 특정 파일
git add hello.txt
```

### 커밋

스테이지에 올라온 파일을 하나의 버전으로 만드는 행위이다. 

```bash
git commit -m "message"
```

### 스테이징 & 커밋 한번에

```bash
git commit -am "message"
```

### 로그 확인 

로그 확인하고 `q` 입력하면 나갈 수 있음.

```bash
git log
```
