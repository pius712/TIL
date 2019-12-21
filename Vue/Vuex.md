# Vuex

* 복잡한 애플리케이션의 컴포넌트들을 효율적으로 관리하는 라이브러리  
* Vuex 라이브러리의 등장 배경인 Flux 패턴  
* Vuex 라이브러리의 주요 속성인 state, getters, mutations, actions 학습  
* Vuex를 더 쉽게 코딩할 수 있는 방법인 Helper 기능 소개  
* Vuex로 프로젝트를 구조화하는 방법과 모듈 구조화 방법 소개.

## Flux 패턴?  

MVC 패턴의 복잡한 데이터 흐름 문제를 해결하는 개발 패턴    Unidirectional data flow  

Action -> Dispatcher -> Model -> View 

1. action: 화면에서 발생하는 이벤트 또는 사용자의 입력
2. dispatcher: 데이터를 변경하는 방법, 메서드
3. model: 화면에 표시할 데이터
4. view: 사용자에게 비춰지는 화면

### MVC 패턴과의 비교  

* MVC 패턴  
Controller -> Model  <--> View 양방향 

### MVC 패턴의 문제점  

* 기능 추가 및 변경에 따라 생기는 문제점을 예측할 수가 없음 
* 앱이 복잡해지면서 생기는 업데이트 루프  

![MVC 문제점](../img/MVC.png)

### Flux 패턴의 단방향 데이터 흐름 

* 데이터의 흐름이 여러 갈래로 나뉘지 않고 단방향으로만 처리  

![flux](../img/Flux.png)

___

## Vuex의 필요성

복잡한 애플리케이션에서 컴포넌트의 개수가 많아지면 컴포넌트 간에 데이터 전달이 어려워진다. 000

### 이벤트 버스로 해결?

* 어디서 이벤트를 보냈는지 혹은 어디서 이벤트를 받았는지 알기 어려움.

```javascript
//Login.Vue
eventBus.$emit('fetch`,loginInfo);
//List.vue
eventBus.$on('display', data=> this.displayOnScreen(data));
//Char.vue
eventBus.$emit('refreshData', chartData);
```

컴포넌트 간 데이터 전달이 명시적이지 않음. 

### Vuex로 해결할 수 있는 문제 

1. MVC 패턴에서 발생하는 구조적 오류 
2. 컴포넌트 간 데이터 전달 명시  
3. 여러 개의 컴포넌트에서 같은 데이터를 업데이트 할 때 동기화 문제. 

### VueX 컨셉 

* State : 컴포넌트 간에 공유하는 데이터 `date()`
* View : 데이터를 표시하는 화면 `template`
* Action : 사용자의 입력에 따라 데이터를 변경하는 `methods`  

![vuex 컨셉](../img/concept.png)
단방향 데이터 흐름 처리를 단순하게 도식화한 그림

### Vuex 구조 

컴포넌트 -> 비동기 로직 -> 동기 로직 -> 상태  

![structure](../img/structure.png)

___

설치 & 설정
npm i vuex --save 
`project/src/store/store.js` 생성

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex); 
// vue plugin 기능 전역으로 특정 기능을 추가하고 싶을때 (global functionality)

// Todo.vue 라는 컴포넌트에서 
// this.$store 로 접근이 가능하다?!

export const store = new Vuex.Store({
    // 이 것을 모듈로 만들었기 때문에, 외부에서 import 하면 사용할 수 있다.
});
```

```javascript
import Vue from 'vue';
import App from './App.vue';
import { store } from './store/store.js';

Vue.config.productionTip = false

new Vue({
  store,
  render: h => h(App),
}).$mount('#app')
```

기술 요소  
state : 여러 컴포넌트에 공유되는 `data`
getters : 연산된 state 값을 접근하는 속성 `computed`
mutations : state 값을 변경하는 이벤트 로직. 메서드`methods`
actions : 비동기 처리 로직을 선언하는 메서드 `aysnc methdos`

state란? 

* 여러 컴포넌트 간에 공유할 데이터 - 상태

```javascript
// Vue
data:{
    message: 'Hello vue.js'
}
// Vuex
state:{
    message: 'hello vue.js'
}
```

```HTML

<!-- Vue -->
<p> {{ message }} </p>

<!-- Vuex-->
<p> this.$store.state.message </p>
```  

getters란? 

* state 값을 접근하는 속성이자 `computed()` 처럼 미리 연산된 값을 접근하는 속성

```javascript

state:{
    num:10
},
getters:{
    getNumber(state){
        return state.num;
    },
    doubleNumber(state){
        return state.num*2;
    }
}
```

```HTML
<p> this.$store.getters.getNumber </p>
<p> this.$store.getters.doubleNumber</p>

```

mutations란?

* state의 값을 변경할 수 있는 유일한 방법이자 메서드
* 뮤테이션은 `commit()`으로 동작시킨다. 

```javascript
//store.js
state:{ num: 10},
mutationsL{
    printNumbers(state){
        return state.num
    },
    sumNumbers(state,anotherNum){
        return state.num + anotherNum;
    }
}
//App.vue
this.$store.commit('printNunmbers');
this.$store.commit('sumNumbers',20);
```

mutations의 commit() 형식

* state를 변경하기 위해 mutations를 동작시킬 때 인자(payload)를 전달할 수 있음. (-> payload는 임의의 관행적인 명이고, 객체이다.)

```javascript
// store.js
state: {
    storeNum:10
},
mutations:{
    modifyState(state, payload){
        console.log(payload.str);
        return state.storeNum += payload.num;
    }
}
// App.vue
this.$store.commit('modifystate',{
    str: 'passed from payload',
    num: 20
});

``` 
왜 state는 직접 변경하지 않고 mutations로 변경할까?  
여러 개의 컴포넌트에서 아래와 같이 state 값을 변경하는 경우 어느 컴포넌트에서 해당 state를 변경했는지 추적하기가 어렵다. 

```javascript
method:{
    increaseCounter(){ this.$store.state.counter++ }
}
```

특정 시점에 어떤 컴포넌트가 state를 접근하여 변경한 건지 확인하기 어렵기 때문  
따라서, 뷰의 반응성을 거스르지 않게 명시적으로 상태 변화를 수행. 반응성, 디버깅, 테스팅 혜택. 

왜 mutation은 commit을 통해서 ??  
-->  