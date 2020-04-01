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
(function() {
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
