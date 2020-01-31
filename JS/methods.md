# Methods

## Built-in methods

### call()

`func.call([thisArg[, arg1, arg2, ...argN]])`

`thisArg`: The value to use as this when calling func.

```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

console.log(new Food('cheese', 5).name);
// expected output: "cheese"
```

## Array

- splice()
- slice()
- map
- reduce()
- filter()
- find()
- forEach()

### splice()

### slice()

### map

`arr.map(callback(currentValue[, index[, array]])[, thisArg])`

```javascript
var kvArray = [
  { key: 1, value: 10 },
  { key: 2, value: 20 },
  { key: 3, value: 30 },
];

var reformattedArray = kvArray.map(function(obj) {
  var rObj = {};
  rObj[obj.key] = obj.value;
  return rObj;
});
// reformattedArray는 [{1:10}, {2:20}, {3:30}]

// kvArray는 그대로
// [{key:1, value:10},
//  {key:2, value:20},
//  {key:3, value: 30}]
```

### reduce

```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15

console.log(array1.reduce((acc, cur) => acc + cur));
```

위와 같이 작동하는 메소드. 2번째 인자에는 `initialNumber`가 들어가는데 배열이 비어있는데 초기값을 지정하지않으면 에러가난다. 그리고 설정을 하지 않는 경우에는 배열의 첫번째 요소(인덱스가 0)인 요소를 초기값으로 두고 인덱스가 1인 요소부터 누산한다.  
[참고-Mdn](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

### filter()

`arr.filter(callback(element[, index[, array]])[, thisArg])`

_반환값(return)_  
테스트를 통과한 요소로 이루어진 새로운 배열. 어떤 요소도 테스트를 통과하지 못했으면 빈 배열을 반환합니다.

```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);
// words.filter(function(word){
    return word.length>6;
})
console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

filter()는 배열 내 각 요소에 대해 한 번 제공된 callback 함수를 호출해, callback이 _`true로 강제하는 값을 반환하는 모든 값이 있는 새로운 배열을 생성합니다.`_ callback은 할당된 값이 있는 배열의 인덱스에 대해서만 호출됩니다; 삭제됐거나 값이 할당된 적이 없는 인덱스에 대해서는 호출되지 않습니다. callback 테스트를 통과하지 못한 배열 요소는 그냥 건너뛰며 새로운 배열에 포함되지 않습니다.

### find

```javascript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: 12
```

### forEach

```js
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

## Object

### `delete`

```javascript
const Employee = {
  firstname: 'John',
  lastname: 'Doe',
};

console.log(Employee.firstname);
// expected output: "John"

delete Employee.firstname;

console.log(Employee.firstname);
// expected output: undefined
console.log(Employee);
```

```bash
> "John"
> undefined
> Object { lastname: "Doe" }
```

### `entries`

```javascript
const object1 = {
  a: 'somestring',
  b: 42,
};

for (let [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}
// expected output:
// "a: somestring"
// "b: 42"
for (let entry of Object.entries(object1)) {
  console.log(entry);
}
//["a: somestring"]
//["b: 42"]
```
