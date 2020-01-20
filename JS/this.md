# this

## 함수 호출 시

```js
function foo() {
  console.log(this);
}
foo();
```

--> window 객체 // node에서는 global 객체

## 객체의 메서드 this

```js
var logName = function() {
  console.log(this.name);
};

var myObj = {
  name: 'foo',
  sayName: logName,
};

var otherObj = {
  name: 'bar',
};
otherObj.sayName = logName;

myObj.sayName();
otherObj.sayName();
```

```shell
foo
bar
```

## 내부함수

```js
var value = 100;
var myObj = {
  value: 1,
  func1: function() {
    this.value++;
    console.log('func1 called', this.value);
    func2 = function() {
      this.value++;
      console.log('func2 called', this.value);
    };
    func2();
  },
};
```

```bash
func1 called 2
func2 called 101
```

위와 같은 경우에는 객체 내의 `func1`의 this는 자신의 객체를 가리키는 반면에,
내부 함수 `func2`는 전역 객체인 `window`를 가리키게 된다.

## 생성자 함수

---

**note**
생성자 함수는 js에서 객체를 만드는 방식이다.

---

```js
function Bar() {
  console.log(this);
}
```

--> Bar()를 가리킴.

## 분석

vue js에서 this 사용 분석.

```js
export default {
  data() {
    return {
      users: [],
    };
  },
  created() {
    console.log('first', this);
    axios
      .get('')
      .then(function(res) {
        console.log('second', this);
        this.users = res.data;
      })
      .catch(err => {
        console.error(err);
      });
  },
};
```

`첫번째 this`는 객체의 메서드에 있는 this이다. 따라서 이 this는 자신의 객체를 가리키게 된다. 따라서 이 경우에는 VueComponent가 된다.  
`두번째 this`는 메서드 내에서의 함수 호출이다. 이때 undefind가 되는데... 이 부분은 잘 모르겠다.
