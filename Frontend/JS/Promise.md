# 프로미스

## 콜백 헬

```javascript
Users.findOne('foo', (err, user) => {
  if (error) {
    return console.log(error);
  }
  console.log(user); // 논 블록킹으로 실행이 되어서 completed가 먼저 찍히고 이후에 user가 찍힌다.
  Users.update('foo', 'bar', (err, updatedUser) => {
    if (err) {
      return console.log(err);
    }
    console.log(updatedUser);
    Users.remove('bar', (err, removedUser) => {
      if (err) {
        return console.log(err);
      }
      console.log(removeUser);
    });
  });
});
console.log('completed?');
```

이런 식으로 계속 들어가는 것을 콜백 헬이라고 부른다. 이를 해결하기 위해서는 과거에는 이를 함수로 빼는 시도를 했었다고 한다...;

```javascript
const afterRemove = (err, removedUser) => {
  console.log(removedUser);
};

const afterUpdate = (err, updatedUser) => {
  console.log(updatedUser);
  Users.remove('bar', afterRemove);
};

Users.findOne('foo', (err, user) => {
  if (err) {
    return console.error(err);
  }
  console.log(user);
  Users.update('foo', 'bar', afterUpdate);
});
```

## Promise

```javascript
Users.findOne('foo')
  .then(user => {
    console.log(user);
    return Users.update('foo', 'bar');
  })
  .then(updatedUser => {
    console.log(updatedUser);
    return Users.remove('bar');
  })
  .then(removedUser => {
    console.log(removeUser);
  })
  .catch(err => {
    console.error(error);
  });
```

```javascript
const add = new Promise((resolve, reject) => {
  const a = 1;
  const b = 2;
  if (a + b > 2) {
    resolve(a + b); // 이 resolve와 reject 안에 메세지를 넣어 보낸다.
  } else {
    reject(a + b);
  }
});

add()
  .then(success => {
    console.log(success);
  })
  .catch(fail => {
    console.log(fail);
  });
```

cf) 프로미스를 사용할 수 있는 이유?  
--> 라이브러리가 내부적으로 프로미스를 사용할 수 있도록 지원하기 때문임.

```javascript
/*
    중략
        */
return new Promise((res, rej) => {
  // 생략...
});
```

```javascript
const condition = true;
const promise = new Promise((resolve, reject) =>{
    if(condition){
        resolve('성공');
    }else{
        reject('실패');
    }
}
});

promise
    .then((message)=>{
        console.log(message);
    })
    .catch((error)=>{
        console.error(error);
    })
```

```javascript
promise
    .then((message)=>{
        return new Promise((res,rej)=>{
            res(message);
        });
    })
    .then((message2)=>{  // 여기에 있는 message2의 경우에는 매개변수라서 위의 return 의 res 안의 값과 같을 필요는 없다. 그냥 전달된다는 것을 시각적으로 보여주기 위함.
        return new Promise((res,rej)=>{
            res(message2);
        });
    })
    .then((message3)=>{
        return new Promise((res,rej)=>{
            res(message3);
        });
    })
    .catch((error)=>{
        console.error(error);
    })
```

아래와 같이 함수로 뺄 수도 있다.

```javascript
const handleMessage = (meesage)=>{
    return new Promise((res,rej)={
            res(message);
        });

};
const handleMessage2 = (message2) =>{
    return new Promise((res,rej)={
            res(message2);
        });
};
promise
    .then(handleMessage)
    .then(handleMessage2)
    .then((message3)=>{
        return new Promise((res,rej)={
            res(message3);
        });
    })
    .catch((error)=>{
        console.error(error);
    })

```

## then()

기본 구조
```js
p.then(onFulfilled, onRejected);

p.then(function(value) {
  // 이행
}, function(reason) {
  // 거부
});
```
---
**참고**  
then 메서드에 첫번째 인자로 들어오는 함수의 파라미터는 이행 값(fulfillment value)로 프로미스 객체 안의 값이다.

---

`then()` 메서드는 Promise를 리턴한다. 이 메서드의 인자는 2개의 콜백함수로 구성되는데, 첫번째는 프로미스가 성공했을 경우, 두번째는 실패했을 경우에 시행된다.  
이 메서드는 Promise를 리턴한다. then() 메서드 내에서 값을 리턴하면, 아래와 같은 방식으로, Promise 객체를 반환하는데 내부에 값을 지니게 된다.  
(1.returns a value, the promise returned by then gets resolved with the returned value as its value.
2.doesn't return anything, the promise returned by then gets resolved with an undefined value.)

```js
const resolvedProm = Promise.resolve(33);

let thenProm = resolvedProm.then(value => {
    return value;
```

```bash
jsPromise {[[PromiseStatus]]: "resolved", [[PromiseValue]]: 33}`
```

### vue 코드 분석

```js
//store/actions.js
FETCH_NEWS(context) {
  fetchNewsList()
    .then(res => {
      context.commit('SET_NEWS', res.data);
      console.log('actions');
      console.log(res);
      return res;
    })
    .catch(err => {
      console.error(err);
    });
},
//pages/Newsview.vue
created() {
  // ...
    this.$store
      .dispatch("FETCH_NEWS")
      .then(result => {
        bus.$emit("end:spinner");
        console.log("result");
        console.log(result);
        return result;
      })
      .catch(err => {
        console.error(err);
      });
);

// api/index.js
function fetchNewsList() {
  // return axios.get('https://api.hnpwa.com/v0/news/1.json');
  // --> 아래와 같이 공통된 부분을 빼서 다른 변수로 뺄 수 있다.
  console.log('api call');
  return axios.get(`${config.baseUrl}news/1.json`);
}
```

```bash
// 결과
api call
result
undefined
actions
{data: Array(30), status: 200, statusText: "", headers: {…}, config: {…}, …}
```

왜 why? [참고 Mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)  
dispatch() -> fetchNews() -> fecthNewsList() -> axios.get() -> 여기서 dispatch의 then이 먼저 수행된다.
fetchNews() then이 먼저 수행될 것 같지만, Promise의 resolve()가 호출된다고 해도, then() 메서드 내의 핸들러는 비동기적으로 처리가 된다. 따라서 먼저 큐에 들어가 있던 dispatch의 then()안의 핸들러가 수행되는 것이다.

### 해결방법

아래와 같이 return을 붙이게 되면, 아래의 로직이 모두 수행된 다음에 값이 return된다. (이 값은 Promise이다.) 따라서 이 값이 dispatch의 then()의 핸들러의 인자 값으로 들어가게 된다.

```js
//store/actions.js
FETCH_NEWS(context) {
  return fetchNewsList()
    .then(res => {
      context.commit('SET_NEWS', res.data);
      return res;
    })
    .catch(err => {
      console.error(err);
    });
},
```

## 콜백과 프로미스 차이점

콜백

```javascript
Users.findOne('foo', (err,user)=>{
    console.log(user);
})
```

프로미스

```javascript
const foo = Users.findOne('foo');
/* 
   다른 로직들...
            */
foo.then(z => {
  console.log(z);
}); // 받아오는 곳과 사용하는 곳이 분리되어 있다.
```

promise.all

```javascript
Promise.all([Users.findOne(), Users.remove(), Users.update()])
  .then(result => {})
  .catch(err => {}); //하나라도 실패시 x
```

## Asnyc/await

```js
const value = await expression
```
await expresssion의 반환값은 promise의 resolved 값으로 처리된다. 
The resolved value of the promise is treated as the return value of the await expression.

프로미스

```javascript
Users.findOne('foo')
  .then(user => {
    console.log(user);
    return Users.update('foo', 'bar');
  })
  .then(updatedUser => {
    console.log(updatedUser);
    return Users.remove('bar');
  })
  .then(removedUser => {
    console.log(removeUser);
  })
  .catch(err => {
    console.error(error);
  });
console.log('completed?');
```

Async/await

```javascript
async func() =>{ //func라는 함수
    try{
        const user = await Users.findOne('foo');
        console.log(user);
        const updatedUser = await Users.update('foo', 'bar');
        console.log(updatedUser);
        const removedUser = await Users.remove('bar');
        console.log(removedUser);
        console.log('completed?');
    } catch(err){
        console.log(err);
    }
}
func();
```

프로미스의 경우에는 `completed?`가 먼저 실행된다. 하지만 `async/await`에서는 이 순서를 바꿀 수 있다.  
그리고 에러 발생 예외처리를 해주어야 한다.

async 함수는 Promise 객체를 반환한다. Promise 객체 내부의 값은 async 함수에서 return한 값이 들어간다. 

```js
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}
async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
  return "??";
  // expected output: 'resolved'
}

const temp = asyncCall();
console.log('temp', temp);
```

위와 같이 실행을 하고 temp를 log로 찍으면 "??" 값을 가진 Promise를 반환한다. 