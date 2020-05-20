# Webpack

## Background

```html
  <script src="./math.js">
  <script src="./economics.js">
```

이런 식으로 사용을 하면, 전역 스코프가 적용이 된다.  
따라서, 이를 즉시 실행함수로 만들어주는 방식이 생겼다.

```js
// math.js
var math = math || {};
(function () {
	function sum(a, b) {
		return a + b;
	}
	math.sum = sum;
})();

// app.js
console.log(math.sum(1, 2));
```

### CommonJS

### AMD

### 표준 모델 시스템(현재 사용하는 방식)

```js
// math.js
export function sum(a, b) {
	return a + b;
}
// app.js
import * as math from './math.js';
import { sum } from './math.js';

console.log(math.sum(1, 2));
```

## webpack

mode, entry, output은 필수적으로 설정해줘야 한다.

### install

`npm install -D webpack webpack-cli`

### help

`node_modules/.bin/webpack --help`

### --mode

`"development" "production" "none"

### --entry

### --output

저장하는 경로

`node_modules/.bin/webpack --mode development --entry ./src/app.js --output dist/main`  
-> 이 명령어를 package.json  
"script" :{
"build" : "webpack"
}
이런 방식으로 등록하면 webpack.config.js 파일을 참조해서 실행한다(번들링을 한다).

```js
// webpack.config.js

module.exports = {
	mode: 'development',
	entry: {
		main: './src/app.js'
	},
	output:{
		path: path.resolve('./dist'),
		filename '[name].js', // 동적으로 이름을 만들어준다.
	}
}
```
