# npm

## command

* `npm init` - 프로젝트 초기화. 
package.json 파일에 `npm install`시 dependencies에 추가 된다.

* `npm install express` 와 같이 외부 모듈을 다운로드를 받음
node-modules 폴더에 설치된다.  의존하고 있는 다른 라이브러리도 모두 다운로드한다. 

package.json 파일에 script를 통해서 ..! 

```json
{
    /* .. */
    "scripts":{
        "start": "node index.js"
    }
}
```


* 개발 시 사용하는 모듈  
`--save-dev === -D` 

* 전역으로 설치하여 터미널에서 명령어처럼 사용할 수 있다.  
`--global === -g` 

* 설치된 모듈 삭제  
`npm remove 모듈명` === `npm rm 모듈명`  

* 의존하고 있는 모듈을 보여준다. 
`npm ls 모듈명`

* npm 로그인  
`npm adduser`

* 접속한 계정 확인/ 로그아웃
`npm whoami`/ `npm logout`

* 패키지 버전 업  
`npm version minor`  
`npmv version patch`

* 배포하기  
`npm publish`

* 삭제하기  
`npm unpublish 이름` 