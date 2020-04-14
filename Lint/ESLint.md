# ESLint

- 포맷팅
- 코드 품질

##

.eslintrc.js 파일 생성

## Rules

```js
//.eslintrc.js
module.exports = {
	rules: {
		'no-unexpected-multiline': 'error',
		'no-extra-semi': 'error',
	},
};
```

```zsh
npx eslint app.js --fix
```

자동으로 수정해주는.. rules를 보면 fix 옵션이 있는 경우도 있고 없는 경우도 있다.

```js
module.exports = {
	extends: ['eslint:recommende'],
};
```

위와 같이 extends를 사용하면 여러개의 rules를 상속받아서 적용한다.

```zsh
npx eslint --init
```
