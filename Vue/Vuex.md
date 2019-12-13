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

#### MVC 패턴의 문제점  
* 기능 추가 및 변경에 따라 생기는 문제점을 예측할 수가 없음 
* 앱이 복잡해지면서 생기는 업데이트 루프 
![MVC 문제점](../img/MVC.png)

#### Flux 패턴의 단방향 데이터 흐름 
* 데이터의 흐름이 여러 갈래로 나뉘지 않고 단방향으로만 처리  

![flux](../img/Flux.png)

## Vuex
### 이벤트 버스로 해결?

* 어디서 이벤트를 보냈는지 혹은 어디서 이벤트를 받았는지 알기 어려움.

```javascript
//Login.Vue
eventBus.$emit('fetch`,loginInfo);
//List.vue
eventBus.$ont('display', data=> this.displayOnScreen(data));
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

