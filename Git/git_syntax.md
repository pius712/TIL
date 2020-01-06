# Git

1. 버전관리
2. 브랜치 

## 버전 관리

### 동작 원리

작업 트리 -> 스테이지 -> 저장소

git은 한번이라도 commit을 하게 되면, 그 파일에 대한 수정 여부를 지속적으로 체크한다. git status 명령어 -> tracked file, untracked file.

### 파일의 상태

untracked -> unmodified -> modified -> staged

* untracked -> staged  
:git add 시에 untracked 파일이 staged된다. 
* unmodified -> modified  
: 수정시
* modified -> staged  
: add시
* staged -> unmodified  
: 커밋할 경우


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
// 옵션이 없으면 커밋의 author, data, message 만 나온다.
git log
// 아래의 옵션을 붙이면 커밋에 관련된 파일까지 보여준다. 
git log --stat
//한 줄로 커밋 로그를 알려준다.
git log --oneline
// 각 브랜치의 커밋을 보는 법
git log --branches // git log --oneline --branches
// 그래프로 보는 법
git --branches --graph // --oneline 옵션 가능
```

## gitignore

아래와 같이 `.gitignore` 파일을 생성하면, textfile.txt 파일 제외/node_modules 디렉토리 제외/ .png 확장자를 관리하지 않는다. 

```bash
// .gitignore
textfile.txt
node_modules/
.png
```

## Branch

### branch 만들기

```bash
// 아래는 브랜치를 확인하는 명령
git branch
// 아래와 같이 뒤에 브랜치 이름을 넣으면 브랜치를 추가.
git branch myBranch
```

### branch 전환

```bash
git checkout myBranch
```

### log

``` bash
// 각 브랜치의 커밋을 보는 법
git log --branches // git log --oneline --branches
// 그래프로 보는 법
git --branches --graph // --oneline 옵션 가능
// 브랜치 사이의 차이점 보기.
git log master..apple //master에는 없고 apple 브랜치에는 있는 커밋
```