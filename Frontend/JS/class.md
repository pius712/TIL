# Class

ES6에 도입된 Class 문법
JS의 class는 기존의 prototype 베이스에 syntatical sugar를 더한 것 뿐, 새로운 객체지향 모델이 추가된 것은 아니다. 

## 클래스 선언

클래스는 실제로 특별한 함수일 뿐이다.  
class 문법에는 class expression과 class declration이 있다.

1. class declaration

클래스를 정의하는 첫번째 방법은 class declaration이다. 클래스를 선언하기 위해서는 class 키워드를 class의 이름과 함께 사용하면 된다. 

```js
class Foo {
  constructor(bar) {
    this.fooname = bar;
  }
}
const myFoo = new Foo('bar');
```
---
**note**
Hoisting  
일반적인 함수 선언과 클래스 선언의 차이점은 일반 함수 선언은 호이스팅되는 반면, 클래스는 호이스팅이 되지 않는다는 점이다.  
아래와 같은 경우에는 ReferenceError가 발생한다. 

```js
const p = new Rectangle(); // ReferenceError

class Rectangle {}
```

---

2. Class expressions

클래스 표현식은 클래스를 정의하는 다른 방법이다.  
클래스 표현식은 named, unnamed 두 가지가 가능하다.  
named class 표현식에 붙은 이름은 class body의 local이다.  
이는 클래스의 name property를 통해서 얻을 수 있다. 

```js
// unnamed
let Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle"

// named
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle2"
```
## Class body and methdos 

클래스의 바디는 strict mode로 실행이 된다. 

### Constructor

생성자 함수는 클래스를 통해 만들어지는 객체를 만들고, 초기화하는 메소드이다.   
constructor라는 이름의 함수는 클래스에 단 하나만 있을 수 있다.  
생성자 함수에서는 super 키워드를 사용할 수 있다. super class의 생성자를 호출하기 위해서 사용된다. 

### prototype methods

아래는 생성자 함수와, 일반 메서드가 선언되어 있다.

```js
class Car {
  constructor(brand) {
    this.carname = brand;
  }
  present() {
    return "I have a " + this.carname;
  }
}

const mycar = new Car("Ford");
mycar.present();
```

### Static methods

static 키워드는 static method를 정의하는데 사용된다. static methods는 class를 초기화하지 않아도 사용할 수 있는 함수이다. static methods는 종종 utility 함수를 만드는데 사용될 수 있다. 

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
p1.distance; //undefined
p2.distance; //undefined

console.log(Point.distance(p1, p2)); // 7.0710678118654755
```

### Instance properties

인스턴스 프로퍼티는 class methods의 내부에 정의되어야 한다. 

```js
class Rectangle {
  constructor(height, width) {    
    this.height = height;
    this.width = width;
  }
}
```

static data 프로퍼티나 prototype data 프로퍼티는 class body 선언 바깥에 정의되어야 한다.

```js
Rectangle.staticWidth = 20;
Rectangle.prototype.prototypeWidth = 25;
```

## Sub classing with extends

`extends` 키워드는 class 선언문 혹은 class 표현식에서 다른 class의 자식 class를 만들때 사용된다. 

```js
// 부모 클래스
class Animal { 
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}
// 자식 클래스
class Dog extends Animal {
  constructor(name) {
    super(name); 
    // call the super class constructor and pass in the name parameter
  }
  speak() {
    console.log(`${this.name} barks.`);
  }
}
let dog = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```
만약에 자식 클래스에 생성자 함수가 있다면, `this`를 사용하기 전에 `super()` 콜을 해주어야 한다.

