# ES6

* const & let
* Arrow Function
* Enhanced Object Literals
* Modules
* destructuring
* Spread Operator

Babel  
babel은 es6 javascript를 그 이전에 버전으로 변환시켜주는 프로그램.(transpiling)

## ES5 특징

### 변수의 scope

```javascript
var sum = 0;
for(var i=0; i<= 5; i++){
    sum = sum+i;
}
console.log(sum); //15
console.log(i); //5
```

### 호이스팅  

선언한 함수와 변수를 인터프리터가 가장 상단에 있는 것처럼 인식한다.  
함수 표현식은 해당이 안되고, 함수 선언식과 변수는 호이스팅 된다.

```javascript
function foo(){
    return 10;
}
foo(); //5;
function foo(){
    return 5;
}
```

* 함수 선언식

    ```javascript 
    funtion foo(){
        return 10;
    }
    ```

* 함수 표현식

    ```javascript
    var a = function(){
        return 10;
    }
    ```

아래와 같이 작성된 코드는 

```javascript
var sum = 5;
sum = sum + i;
function sumAllNum(){
    //...
}
var i = 10;
```

실제로 동작을 아래와 같이 동작한다.  

```javascript 
var sum;
function sumAllNum(){
    //...
}
var i;

sum =5;
sum = sum + i; 
i = 10;
```

## Const & let

> 블록 단위 `{ }`로 변수의 범위가 제한되었음. 

### const  

> 한번 선언한 값에 대해서 변경할 수 없음(상수 개념)

```javascript
const a = 10;
a = 20; //Uncaught TypeError: Assignment to constant variable.
```

배열이나 객체의 경우에는 내부의 값을 변경할 하는 것은 가능하다. 

```javascript 
const a = {};
a.num = 10;
console.log(a); // {num: 10}

const a = [];
a.push(20);
console.log(a); //[20] 
```

### let  

> 한번 선언한 값에 대해서 다시 선언할 수 없음

```javascript 
let a = 10;
let a = 20; //Uncaught SyntaxError: Identifier 'a' has already been declared
```

```javascript 
let sum = 0;
for(let i=0; i<5; i++){
    sum += i;
}
console.log(sum); // 10
console.log(i); //Uncaught ReferenceError:
```

### ES6 변수 scope

```javascript
function f(){
    {
        let x;
        {   //새로운 블록안에 새로운 x의 스코프가 생김
            const x = "foo";
            x = "boo"; // 위에 이미 const로 x를 선언했으므로 
            // 다시 값을 대입하면 에러 발생
        }
        x = "bar"; //이전의 블록 범위로 돌아왔기 때문에 
        //let x 에 해당하는 메모리에 값을 대입
        let x = "far"; 
        // Uncaught SyntaxError: Identifier 'x' has already been declared
    }
}
```

## Arrow Function

ES5와 ES6 간단한 비교. 

```javascript
var sum = funtion(a, b){
    return a+b;
};

var sum = (a, b)=>{
    return a+b;
}
sum(10, 20);
```

사용 예시 

```javascript
//ES5
var a = ["a", "b", "c"];
arr.forEach(funtion(value){
    console.log(value);
});
```

arr.forEach((v)=>{
    console.log(v);
});


## enhanced Object Literals - 향상된 객체 리터럴  

```javascript
var dictionary = {
    words: 100,
    // ES5
    lookup: function(){
        console.log("find words");
    },
    //ES6
    lookup(){
        console.log("find words");
    }
};
```

* 객체의 속석명과 값 명이 동일할 때 아래와 같이 축약 가능

```javascript
var figures = 10;
var dictionary = {
    //figures: figures
    figures
};
```

* 예시     
   
```html
components:{
// 'TodoHeader': TodoHeader,
// 'TodoInput': TodoInput,
// 'TodoList': TodoList,
// 'TodoFooter': TodoFooter
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
}
```

## Modules

* 자바스크립트 모듈 로더 라이브러리 기능을 js 언어 자체에서 지원.  
자바에서의 클래스나 패키지 같은 개념이라고 생각하면 될 듯.  
* 호출되기 전까지는 코드 실행과 동작을 하지 않는 특징이 있음.  

```javascript
// libs/math.js
export function sum(x, y){
    return x+y;
}
export var pi = 3.14;

//main.js
import {sum} from 'libs/math.js'
sum(1,2);
```

* `default` export
한 개의 파일에서 하나밖에 export가 안된다. 일종의 encapsulation. 

```javascript
//util.js
export default function (x){
    return console.log(x);
}

// main.js
import util from 'util.js';
console.log(util);
util('hig');

//app.js 
import log from 'util.js;
console.log(log);
log('hi');
```

## destructuring

```js
const me = {
    name: 'pius',
    age: 28,
    nationality: 'korea',
    hobby: {
        music : 'jazz',
        movie: 'romance'
    }
}
// const name = me.name;
// const age = me.age;
// const nation = me.nationality;
// const music = me.hobby.music;
// const movie = me.hobby.movie;
const { name, age, nationality: nation, hobby: {music, movie}} = me;
console.log(name, age, nation, music, movie);


```
## Spread Operator

`...` : spread operator

```javascript
let josh = {
  feild: 'web',
  language: 'js',
};

// let develper = {
//   nations: 'korea',
//   field: josh.field,
//   language: josh.language,
// };

let developer = {
  nations: 'korea',
  ...josh
};

console.log(developer);
``` 

```bash
[object Object] {
  feild: "web",
  language: "js",
  nations: "korea"
}
```