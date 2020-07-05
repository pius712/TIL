# generator

es6에 들어온 문법으로, redux-saga에서 사용되는 es6.


## 설명 

```js
function* generator(i) {
  yield i;
  yield i + 10;
}

const gen = generator(10);
// generator 객체 반환.
console.log(gen.next().value);
// expected output: 10

console.log(gen.next().value);
// expected output: 20
```

function* 선언을 통해 genrator function을 정의할 수 있다. 이 함수를 호출하면 generator 객체가 반환된다. 

Generator 함수는 호출되면, Iterator 객체(generator 객체)가 반환된다. Iterator객체의 `next()` 함수를 호출하면 처음에 선언한 generator 함수가 실행되어 yield 문을 만날때까지 진행이 된다.  
그리고 yield 문을 실행되고, 다음의 `next()` 함수를 호출하면 그 위치로 돌아오게 된다. 
 
next() 가 반환하는 객체는 yield문이 반환할 값(yielded value)을 나타내는 value 속성과, Generator 함수 안의 모든 yield 문의 실행 여부를 표시하는 boolean 타입의 done 속성을 갖는다. next() 를 인자값과 함께 호출할 경우, 진행을 멈췄던 위치의 yield 문을 next() 메서드에서 받은 인자값으로 치환하고 그 위치에서 다시 실행하게 됩니다.