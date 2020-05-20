# ESLint

ESLint는 js 코드를 `more consistent and avoiding bugs` 하도록 만들어주는 도구이다. 

1. 포맷팅
2. 코드 품질

- 설치
- 설정파일  
  - rules
  - extends
  - override

## 배우는 이유?

electron을 통해서 간단한 데스크톱 앱을 만들기 위해, cli를 통해 프로젝트를 생성하였다. 이 때, build마다 eslint 에러가 나서 `eslintrc` 파일 설정을 제대로 알기 위해서.

## 설치

```zsh
npm install eslint --save-dev

# or

yarn add eslint --dev
```

설치가 완료된 이후, 아래를 실행하면 configuration 파일이 생긴다.

```zsh
npx eslint --init
```

## 설정 파일

eslint 설정을 하기 위해서는 설정 파일이 필요하다.
`.eslintrc.js`


### Rules

기본적으로 `rules`를 통해서 eslint 규칙들을 설정할 수 있다. rules를 보면 fix 옵션이 있는 경우도 있고 없는 경우도 있다.
 

```js
//.eslintrc.js
module.exports = {
	rules: {
		'no-unexpected-multiline': 'error',
		'no-extra-semi': 'error',
	},
};

# style1
배열의 첫번째 값은 rule에 대한 setting이고, 두번째 값은 옵션이다. 

"rules": {
		"semi": ["error", "always"],
		"quotes": ["error", "double"]
}

# style2 

```


설정한 후, 아래의 코드를 실행하면 고칠 수 있는 코드에 대해서 코드를 수정해준다. 

```zsh
npx eslint app.js --fix
```

자동으로 수정해주는.. 

- enable additional rules
- change an inherited rule's severity without changing its options:
  - Base config: "eqeqeq": ["error", "allow-null"]
  - Derived config: "eqeqeq": "warn"
  - Resulting actual config: "eqeqeq": ["warn", "allow-null"]
- override options for rules from base configurations:
  - Base config: "quotes": ["error", "single", "avoid-escape"]
  - Derived config: "quotes": ["error", "single"]
  - Resulting actual config: "quotes": ["error", "single"]
### extends

```js
module.exports = {
	extends: ['eslint:recommende'],
};
```

위와 같이 extends를 사용하면 여러개의 rules를 상속받아서 적용한다.

```zsh
npx eslint --init
```

### override
