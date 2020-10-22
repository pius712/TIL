# 경험담

file-loader를 돌리면 에러가 난다. file을 찾을 수 없다고 404에러가 난다.

로그를 보면, path설정이 잘못되어 있는 것을 알 수 있다.

왜 이런 오류가 발생하는지 알기 위해서는 웹팩의 실행 순서를 알아야한다.

1. 엔트리 파일을 읽는다.
2. 읽다가 file을 import 하는 부분을 만난다.
3. 웹팩 설정을 읽어서 처리한다.
4. 파일을 아웃풋 폴더에 저장한다.

---

**note**
The publicPath configuration option can be quite useful in a variety of scenarios. It allows you to specify the base path for all the assets within your application.

---

자 아래 파일 구조를 보자.

```zsh
- dist/
- src/
  - images/
    - imagefile(사용되는 이미지 파일)
  - views
    - somefile(이미지를 불러오는 파일)
  - main.css(이미지를 불러오는 파일)
- index.html/
```

파일을 빌드하고 나온 js파일에서는 import하는 경로를 따라갈 것인데, 이미지 파일은 './dist' 폴더에 저장되어 있다.
그러니까, dist/src/images/imagefile 이런식의 참조를 하려고 하는데, 그곳에는 파일이 없다.

이를 변경해줄 수 있는 옵션이 `publicPath`이다.

`publicPath: './dist` 설정을 해주면,  
`dist/main.js` 파일을 빌드할때, 이미지의 참조를 `./dist` 파일아래에서 하게 된다.
