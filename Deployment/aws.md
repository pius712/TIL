# AWS

우선, React, Vue, Node를 아마존에 배포하는 방법에 대해서 알아볼 것이다.

## EC2

Amazon Elastic Compute Cloud (EC2)

EC2에서 인스턴스 생성을 누른다.

Linux를 사용하여 만들어준다. 

보안 그룹에서 http/https를 추가해준다.

키 페어를 생성, 혹은 기존의 것으로 만들어서 다운로드한다. 

## node 설치

### 들어가기전

간단 설명..   
apt란? 
mac OS의 homebrew와 같은 패키지 매니저라고 보면 된다.

아래 먼저 실행...
```
$ sudo apt-get update
$ sudo apt-get install -y build-essential
```
### NVM

nvm으로 설치하는거 자꾸 에러나서..   
[nodejs공식문서](https://github.com/nodesource/distributions/blob/master/README.md)
이거대로하자

---
**note**  
nvm 패키지를 깔때 주의할점.  
aws ec2 인스턴스에 ssh로 접속을하면, root 계정과 ubuntu 계정 두개가 있다. 그런데 이 둘의 path가 달라서 root에서 node 명령어가 수행이 안된다.  
root에 설치해서 root로 작업을 하든, 환경 변수 설정을 해주던가 해야한다.  
mysql 접속이나 이런 부분때문에 그냥 root에서 하는걸로...

---

[아마존 문서](https://docs.aws.amazon.com/ko_kr/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html)  

linux instance로 접속을 한 이후

1. 아래의 명령어를 통해 nvm 설치  
`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash`

2. nvm 활성화  
`. ~/.nvm/nvm.sh`
3. node 최신버전 설치  
`nvm install node`  
Node.js를 설치하면 npm(노드 패키지 관리자)도 설치된다.
4. node -v, npm -v 를 통해서 설치가 잘 되었는지 버전 확인을 한다.

## pm2

node app을 aws ssh로 접속해서 실행하면,   
foreground process라서 터미널에서 나가면 node 서버가 꺼진다.

`npm i pm2`

package.json에서 
script에 
`start: pm2 start app.js` 로 바꿔준다. 

모니터링 하고 싶으면 
`npx pm2 monit` 명령어 수행하면 된다.
이는 pm2가 글로벌로 설치되어있지 않기 때문에, npx로 실행하는 것.

`npx pm2 kill`: 프로세스 종료

 `npx pm2 logs` : 로그
 `npx pm2 logs -error`: 에러 로그
`npx pm2 list`: 프로세스 리스트
`npx pm2 reload all`: 프로세스 재시작 // git pull 이후에 프로세스 굳이 종료 안하고 reload하면 된다.
## front 서버 시작하기

1. 패키지 다운받기.  
`npm i`

2. 빌드  
`npm run build`

3. 시작  
`npm run start`
`npx pm2 start npm -- start`
// npm2 를 통해서 npm start 실행
4. 모니터링
`npx pm2 monit`

## backend 서버

[설치 방법 공식문서](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/)  
[레포지터리 다운 주소](https://dev.mysql.com/downloads/repo/apt)  

여기서 network 탭으로 다운로드 주소 추출해서 아래와 같이 사용하는데.. 다른 방법은 모르겠다. 
1. Add repo

`wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.15-1_all.deb`

`sudo dpkg -i mysql-apt-config_w.x.y-z_all.deb`
x.y.z. 에는 버전이름이 들어간다. 

`sudo dpkg -i mysql-apt-config_0.8.15-1_all.deb`

`sudo apt-get install mysql-server`

2. 
`sudo apt-get install mysql-server`

3. 비밀번호 설정
설치를 완료하고나면 바로 비밀번호 설정할 수 있다. (터미널에 설정창이 뜬다.)
여기서 비밀번호 설정을 해도되고, 비워두고 ok를 하면 이후에 mysql-secure_installation을 통해서 설정이 가능하다. 

루트 계정으로 가서 (`sudo su`)
`mysql_secure_installation`

4. 접속

`mysql -u root -p`

이유는 모르겠는데 이후에 프로그램을 npm run start로 수행하면 access denied 에러가 뜬다. 
이때, sudo mysql -u root
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'test';` 를 해서 비밀번호를 변경해주면 된다. (비밀번호를 설정해줬음에도 mysql에 mysql database에 유저 정보에는 비밀번호가 비어있다.)


바로 실행하면 에러 생기는데...
npx sequelize db:create

아래 에러..? 머지
warning connect.session() memorystore is not designed for a production environment as it will leak

80번 포트 에러  
Error: listen EACCES: permission denied 0.0.0.0:80  
1023번 아래의 포트는 root가 아닌 사용자가 못 연다. 

## 리눅스 명령어...

`wget` 인터넷 파일 다운로드 받는 명령어  

`sudo su` 루트 계정 전환
