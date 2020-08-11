# Nginx

## 들어가기전에
Nginx 쓰려면, 나의 프로그램 서버 포트는 80번이 아니라 다른 포트여야한다. 기본 nginx 설정은 3060이다.

## install 및 환경설정

1. 패키지 관리자를 통해 nginx 설치

```
sudo apt-get install nginx
```
2. 환경설정 파일 확인 가능.  
```
vim /etc/nginx/nginx.conf
```
3. certbot-auto 설치
```
wget https://dl.eff.org/certbot-auto
```
4. certbot-auto 파일에 대한 실행권한 부여
```
chmod a+x certbot-auto
// certbot-auto을 모두가 실행할 수 있도록 권한 부여
// 해당 명령어는 tool/linux/권한관리에서 확인
```
5. cerbot-auto 실행
(원래는 nginx를 먼저 실행하고 해야하는게 맞는듯)
```
./certbot-auto 
// 실행
```
6. 이메일 설정
```
Enter email address:
<!-- 이메일 입력:  -->
```
7. 기존의 서버가 80번 포트 점유시  
```
sudo su
sudo lsof -i tcp:80
```
(나오는 값이 없어야 함, 나온다면 sudo kill -9 프로세스아이디(PID))

```
sudo apt-get install -y nginx
vim /etc/nginx/nginx.conf
```
(여기서 http 안에 server에 여러분 도메인(server_name)과 프록시 포트(3060같은 것)로 작성)

:wq!로 저장

8. nginx 시작
```
sudo systemctl start nginx (정상 실행이면 바로 아무 말 없이 실행)
// 설정 바꾸고 재시작시
// sudo systemctl restart nginx
sudo lsof -i tcp:80 (nginx가 보여야 함)

wget https://dl.eff.org/certbot-auto

chmod a+x certbot-auto

./certbot-auto
```

여러분의 도메인이 보이면 1번 누르면 됨

나중에 갱신하려면 certbot-auto renew (자동화하려면 crontab 명령어 알아보기)

9. certbot-auto 실행 성공시

fullchain.pem, privatekey.pem이 저장된다.



**note**  
certbot?  
간단하게 정리하면 환경에 맞춰 Let’s Encrypt 인증서를 자동으로 발급/갱신해주는 봇입니다. Let’s Encrypt의 인증서 발급 방식을 간단하게 이야기하자면, 인증서 요청 -> 도메인에 대한 소유권 확인 챌린지 -> 발급과 같은 절차를 밟습니다. certbot은 이러한 부분의 처리를 자동으로 수행해줍니다.

---