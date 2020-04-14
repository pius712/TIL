# Prettier

ESlint의 포맷팅 부분을 더 일관성 있게 만들어 주는 도구.

## install

```zsh
npm i prettier
```

## command

```zsh
npx prettier [파일]
npx prettier [파일] --write // 고친 다음 파일에 쓴다.
```

## ESlint와의 통합

### eslint-config-prettier

`npm i eslint-config-prettier`

```js
//.eslintrc.js
//...
"extends": ["eslint:recommended", "eslint-config-prettier"]
//...
```

이렇게 하면 eslint의 규칙 중 prettier와 충돌하는 규칙은 disable 시켜버린다.

### eslint-plugin-prettier

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
