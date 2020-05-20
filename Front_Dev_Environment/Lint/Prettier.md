# Prettier

##  About
ESlint의 포맷팅 부분을 더 일관성 있게 만들어 주는 도구.  
팀 단위의 프로젝트를 할 때, 합의된 코드 스타일을 갖는 것이 중요한데, 이를 자동으로 스타일링 해주는 것이 프리티어이다. 

## install

```zsh
npm install --save-dev --save-exact prettier
# or globally
npm install --global prettier
```

## command

```zsh
npx prettier [파일]
npx prettier [파일] --write // 고친 다음 파일에 쓴다.
```

## ESlint와의 통합

통합하기 위해서는 3가지 방법이 있다. 3번째 방법이 권고된다. 

### Disable formatting rules

`eslint-config-prettier` 은 프리티어와 충돌이 생기는 rules를 비활성화 하는 설정이다. 

`npm i eslint-config-prettier`

설치후에, `.eslintrc.js`에 
```js
//.eslintrc.js
//...
"extends": ["eslint:recommended", "eslint-config-prettier"]
//...
```

이렇게 하면 eslint의 규칙 중 prettier와 충돌하는 규칙은 disable 시켜버린다.

### Use ESLint to run Prettier

`eslint-plugin-prettier`

이 플러그인은 프리티어를 사용해 코드를 포맷팅하는 rule을 Eslint에 합친다. 
이 방법은 prettier의 규칙을 eslint에 합쳐버린다. 

`npm i -D eslint-plugin-prettier`

아래의 부분을 추가해준다.

```js
// .eslintrc.js
{
  plugins: [
    "prettier"
  ],
  rules: {
    "prettier/prettier": "error"
  },
}
```

`npx eslint app.js --fix` 이제 eslint만 실행해도 prettier 부분을 수행한다.


### Recommend config

`npm i -D eslint-config-prettier eslint-plugin-prettier`

두개 모두 설치. 

```
// eslintrc.js
{
  "extends": ["eslint:recommended","plugin:prettier/recommended"]
}
```

## 자동화

ESlint와 Prettier를 통합해도 매번 명령어를 통해서 실행하는 것은 번거롭기 때문에 자동화를 사용하면 좋다.

```
// .vscode/settings.json 
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```