# mail 인증

보통의 회원가입의 경우에는 이메일을 보내서 인증을 하는 시스템을 갖추고 있다.  
이러한 인증 프로세스를 위해서 nodemailer 라는 라이브러리를 사용한다.

## 메일 인증 프로세스

회원가입 -> 가입 대기 상태 -> 이메일 sending (인증번호와 함께) -> 이메일 인증(사용자가 인증번호 입력) -> 가입 완료


## Nodemailer

Nodemailer는 Node.js application의 모듈로서, email sending을 쉽게 만들어준다.  

### 설치

`npm install nodemailer`


### Usage

이메일을 보내기 위해서는 아래와 같이 transporter 객체가 필요하다 
`let transporter = nodemailer.createTransport(transport[, defaults])`

- `transporter` : 메일을 보낼 수 있도록 하는 객체 
- `transport`: transport 환경설정 객체, connection url 또는 plugin 인스턴스이다
- `defaults` : mail options를 위한 default 값 객체이다.


 `transporter` 객체는 한번만 만들면 된다. 그리고 이를 가지고 계속 사용할 수 있다.