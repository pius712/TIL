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
git log --branches --graph // --oneline 옵션 가능
// 여기서 (--branches === --all) 
// 브랜치 사이의 차이점 보기.
git log master..apple //master에는 없고 apple 브랜치에는 있는 커밋
```

### 브랜치 병합 

브랜치를 병합하려면 마스터 브랜치에서 병합을 해야한다.  
|  
|_master  
|_apple  

```bash
git merge apple
``` 

명령을 하게 되면 합쳐진다.  
문제는 병합시, master 브랜치와 apple 브랜치가 같은 파일의 같은 부분을 동시에 수정했을때 생긴다. 이를 `conflict`라고 한다.  
충돌이 발생하면 충돌이 발생한 파일에 들어가면  

```bash
<<<<<<<<<<Head
master content 2
=========
apple content 2
>>>>>>>>>apple
```` 

이런 식으로 나타나고, `Head` 의 아래 부분은 현재 브랜치에서 수정한 내용.  
 `apple` 위의 부분은 apple 브랜치가 수정한 내용이 나타난다.  
 <, =, > 부호는 모두 지우고, 충돌난 부분의 내용을 원하는 방향으로 수정하고 저장하면 된다. 그리고 다시 스테이지에 올리고, 커밋을 하면된다.

 ```bash
 git add .
 git commit -m "message"
 ```
 
 병합이 끝난 후에 사용하지 않는 브랜치는 마스터 브랜치에서 아래와 같이 실행하면 된다. 병합하지 않은 브랜치를 강제로 삭제하려면 `-D` 옵션을 붙이면 된다.
 
 ```bash
 git branch -d o2
 ```
