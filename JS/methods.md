# Methods

## Array

### splice()

### slice()

### filter()

`arr.filter(callback(element[, index[, array]])[, thisArg])`

*반환값(return)*  
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

filter()는 배열 내 각 요소에 대해 한 번 제공된 callback 함수를 호출해, callback이 *`true로 강제하는 값을 반환하는 모든 값이 있는 새로운 배열을 생성합니다.`* callback은 할당된 값이 있는 배열의 인덱스에 대해서만 호출됩니다; 삭제됐거나 값이 할당된 적이 없는 인덱스에 대해서는 호출되지 않습니다. callback 테스트를 통과하지 못한 배열 요소는 그냥 건너뛰며 새로운 배열에 포함되지 않습니다.

## Object

`delete`

```javascript
const Employee = {
  firstname: 'John',
  lastname: 'Doe'
}

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