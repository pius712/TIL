# Object

Object class는 자바스크립트의 data type 중 하나이다.

js의 객체는 모두 `Object.prototype`을 상속한다. 

한 '객체의 프로토타입'은 각 인스턴스가 가지는 property(__proto__를 통해 접근가능한)이고, 생성자 함수의 'prototype property'는 해당 생성자 함수의 프로퍼티라는 것이다. 즉, 같은 곳을 가리키고 있다. (아마 객체와 인스턴의 차이? 결국 같은 것을 보는 시각에 따라 다르게 부르는 것과 비슷한것 같다. )



자~ `prototype`는 그 객체의 인스턴스가 어디서 왔는가?를 나타낸다. 그러니까 `prototype property`와 관계 없이, 해당 인스턴스의 prototype을 가리키는 말이다. 이를 확인하기 위해서는 `__proto__`라고 하는 property를 통해서 알 수 있다. 

`prototype property`는 말 그대로 프로퍼티인데 이 프로퍼티는 객체이고 이 객체에는 상속되고자 하는 members를 정의할 수 있다. 


한 객체의 프로토타입과 생성자 함수의 prototype property와의 차이??


It's important to understand that there is a distinction between an object's prototype (available via Object.getPrototypeOf(obj), or via the deprecated __proto__ property) and the prototype property on constructor functions.

The former is the property on each instance, and the latter is the property on the constructor. That is, Object.getPrototypeOf(new Foobar()) refers to the same object as Foobar.prototype.

```js
var o = {}; 
```
이 `o` 객체는 현재 Object.prototype을 **상속** 한다.  
그리고 `o` 객체의 프로토타입은 Object이다. 

