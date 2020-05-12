# code splitting

## 필요성

코드 스플릿을 통해서 코드를 여러 개의 번들로 나누게 되어, 필요시에 로딩 되도록 한다. SPA의 경우에 웹팩이 하나의 파일로 번들링하게 되면, 페이지의 크기가 커질 수록 초기에 로딩하는 시간이 길어지는데 코드 스플릿을 하면 이를 줄일 수 있다.

## Vue에 적용

1. Async 

[Async Components/공식 사이트](https://vuejs.org/v2/guide/components-dynamic-async.html#Async-Components)

```javascript
Vue.component('async-webpack-example', function (resolve) {
  // This special require syntax will instruct Webpack to
  // automatically split your built code into bundles which
  // are loaded over Ajax requests.
  require(['./my-async-component'], resolve)
})
```
factory function에 resolve 콜백함수를 받고 컴포넌트가 필요할 때, resolve 함수가 실행되면서 컴포넌트를 서버로부터 불러온다. 

2. dynamic import

```js
import('./Foo.vue') // returns a Promise
```


위의 두 방식을 합치게 되면 아래와 같이 만들 수 있다. 
```javascript
// routes/index.js
import Vue from 'vue';
import VueRouter from 'vue-router';
Vue.use(VueRouter);

export default new VueRouter({
	mode: 'history',
	routes: [
		{
			path: '/login',
			component: () => import('@/components/LoginPage.vue'),
		},
		{
			path: '/signup',
			component: () => import('@/components/SignupPage.vue'),
		},
	],
});

```
