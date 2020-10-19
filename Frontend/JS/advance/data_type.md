# Data Type

자바스크립트의 Type은 2가지로 나누어진다. `원시 값`/`객체`

## 원시 값

원시 값으로는 `number`/`string`/`boolean`/`null`/`undifine`가 있다.

하지만, `"hello world".toUpperCase()`는 어떻게 수행되는가?

일반적으로 `number`/`string`의 경우에는 프로퍼티를 호출할 수 있다.  예를들어 `.len / .substring()`.  
이 때, 래퍼(wrapper) 객체의 개념이 나온다. 만약, 위의 원시 값에 대한 프로퍼티를 참조하려고 하면 내부적으로 래퍼 객체를 생성하게 된다.

```js
var a = "hello world";
a.toUpperCase();
// -> new String(a) -> 이후 프로퍼티 호출. 
```

이 래퍼 객체는 프로퍼티 참조시에 생성되었다가, 이후에는 바로 제거된다. (프로퍼티는 기본적으로 readonly처럼 작동하게 된다.) 
따라서 위의 예시에서 `a.len = 20`과 같은 코드를 호출해도, 호출 이후 바로 래퍼 객체가 사라지기 때문에, 의미 없는 코드가 되는 것이다. 
