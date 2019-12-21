## Command

* ls - 특정 디렉터리의 내용을 나열  
options
  * -a - 숨김 파일을 포함한 모든 파일 출력(all)
  * -l - 자세한 내용 출력(long) 
  * -s - 파일 크기 순대로 정렬(size)
* cd - 다른 디렉터리로 변경(DOS에서처럼)
* sudo - 추가적인 보안 권한을 얻기 위해 수퍼유저로 인증
* mkdir 이름 - 새로운 디렉토리 추가 
* rmdir 이름 - 현재 경로에서 이름에 해당하는 폴더 지우기
* rm [option] filename  
    option  
  * -f : 쓰기권한(수정, 추가 삭제)이 없더라도, 묻지말고 지우기
  * -i : 물어보고 지우기 (-I : 여러파일을 지울땐 한번만 물어보기)
  * -r : 디렉토리 및 그 안의 모든 파일 지우기(reculsive의 약자)
  * -rf : (-f 옵션 + -r 옵션)

* ifconfig - ip에 관련된 정보
* ps - 현재 실행중인 프로세스 

* `>` - echo 문자열 > 파일이름  
ex) echo hello > README.MD

* command + shift + '.' - 숨김 파일 보기/끄기 

* curl
다양한 프로토콜로 데이터를 전송하는..
ex) curl -X GET 'localhost:3000/' 