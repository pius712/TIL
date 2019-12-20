# npm

`npm init` - 프로젝트 초기화. 
package.json 파일에 `npm install`시 dependencies에 추가 된다.

`npm install express` 와 같이 외부 모듈을 다운로드를 받음
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