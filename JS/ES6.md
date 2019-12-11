
Babel  
babel은 es6 javascript를 그 이전에 버전으로 변환시켜주는 프로그램. 
## ES6

### ES5 특징  
#### 변수의 scope
```javascript
var sum = 0;
for(var i=0; i<= 5; i++){
    sum = sum+i;
}
console.log(sum); //15
console.log(i); //5
```
#### 호이스팅  
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
### Const & let
#### const  
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
#### let  
>   한번 선언한 값에 대해서 다시 선언할 수 없음
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

#### ES6 변수 scope
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
### Arrow Function

### enhanced Object Literals

