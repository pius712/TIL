# 변수

## const, let

const와 let은 블럭({}) 스코프

const는 상수 값을 재할당 할 수 없다.  
const는 처음부터 값을 초기화해야한다.

```javascript
const h = [1, 2, 3, 4, 5];
h[0] = true;
h[1] = false;
console.log(h);
```

```bash
[true, fasle, 3,4,5]
```

객체가 할당된 경우에는 객체 내부 속성은 바꿀 수 있다.

let은 다시 선언 불가능.

## 템플릿 문자열

```javascript
const a = 'hello';
const b = true;
const c = 3;
const d = `${a}의 값은  ${b}이고 ${c}몰라요`;
```

## 객체 리터럴

```javascript
var sayNode = function() {
  console.log('Node');
};
var es = 'ES';
var oldObject = {
  sayJS: function() {
    console.log('JS');
  },
  sayNode: sayNode,
};
oldObject[es + 6] = 'Fantastic'; // 동적으로
```

```javascript
const newObject = {
  sayJS() {
    console.log('JS');
  },
  sayNode, //키와 값이 같은 경우에는 이렇게 가능.
  [es + 6]: 'Fantastic',
};

newObject.sayNodE(); //Node
newObject.sayJS(); //JS
console.log(newObject.ES6);
```

## 화살표 함수

```javascript
function add1(x, y) {
  return x + y;
}

const add2 = (x, y) => {
  return x + y;
};

const add3 = (x, y) => x + y;
//바로 리턴하는 경우에는 return 키워드 없이 그냥 사용해도 됨.
```

function과 화살표 함수의 차이는 `this`.

```javascript
var relationship1 = {
  name: 'pius',
  friends: ['foo', 'bar', 'zoo'],
  logFriends: function() {
    var that = this; // relationship1 을 가리키는 this를 that에 저장.
    this.friends.forEach(function(friend) {
      console.log(that.name, friend);
    }); //만약에 콘솔에 this를 찍으면 window객체가 찍히게 된다.
  },
};
```

```javascript
const relationship2 = {
  name: 'pius',
  friends: ['foo', 'bar', 'zoo'],
  logFriends() {
    this.friends.forEach(friend => {
      console.log(this.name, friend);
    });
  },
}; // 화살표 함수에서의 this는 relationship2 객체가 된다.
```

## 비구조화 할당

```javascript
const candyMachine = {
  status: {
    name: 'node',
    count: 5,
  },
  getCandy() {
    this.status.count--;
    //console.log(this);
    return this.status.count;
  },
};

// var status = candyMachine.status;
// var getCandy = candyMachine.getCandy
// 위으 코드를 아래와 같이 바꿀 수 있다.
const { status, getCandy } = candyMachine;
status;
getCandy();
```

위의 경우에 getCandy는 호출해도 안 듣는데 그 이유가 원래 객체 내의 `this`가 그 객체에 바인딩 되어있는데, 분리하여 할당하는 순간, console.log(this); 를 해보면 이 `this`가 윈도우 객체를 가리키게 된다는 것을 알 수 있다.

### 비구조화 할당 시, 이름 부여

```js
let obj = {
  name: 'Some Name',
  age: '42',
  gender: 'coder',
};
let { name: foo, ...rest } = obj;
console.log({ foo, rest }); // { foo: 'Some Name', rest: { age: 42, gender: 'coder' } }
//
```

## rest, spread

```javascript
var array = ['nodejs', {}, 10, true];
var node = array[0];
var obj = array[1];
var bool = array[array.length - 1];
```

아래의 코드와 같다.

```javascript
const array = ['nodejs', {}, 10, true];
const [node, obj, , bool] = array;
```

```javascript
const array = ['nodejs', {}, 10, true];
const [node, obj, ...bool] = array;

bool >>> [10, true];
```

```javascript
const foo = (x, ...y) = > console.log(x, y);
foo(5,6,7,8);
>>> 5 [6,7,8,9] // 이런식으로 ...y는 배열에 담긴다.
```
