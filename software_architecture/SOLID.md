# SOLID 설계원칙

SOLID 원칙은 클래스(함수와 데이터 구조)를 배치하는 방법에 대해 설명한다.

- 변경에 유연하다
- 이해하기 쉽다
- 컴포넌트의 기반이 된다

1. SRP (단일 책임 원칙, single responsibility principle)
2. OCP (개방-폐쇄 원칙, open-closed Principle)
3. LSP (리스코프 치환 원칙, Liskov Subsitituion Principle)
4. ISP (인터페이스 분리 원칙, Interface Segregation Principle)
5. DIP (의존성 역전 원칙, Dependency Inversion Principle)

## SRP

**단일 모듈은 변경의 이유가 하나, 오직 하나뿐이어야한다.**  
즉, 하나의 모듈은 오직 하나의 사용자 또는 이해관계자에 대해서만 책임져야 한다.

모듈은 무엇이고, 그 변경의 이유는 무엇인가?

모듈 : 모듈은 간단히 말하자면 소스파일을 뜻한다.
변경의 이유: Actor(변경을 요청하는 집단, e.g 사용자와 이해관계자)

### SRP 원칙의 위배 징후

1. 우발적 중복

```js
class Employee {
  caclulatePay() {}
  reportHours() {}
  save() {}
}
```

위의 Employee 클래스는 3개의 메서드가 있다.
위의 메서드 중 `calculatePay`는 회계팀에서 기능을 정의, CFO에 보고를 위해 사용된다.
`reportHours` 메서드는 인사팀에서 기능을 정의, COO에 보고를 위해 사용된다.
`save` 메서드는 DBA가 기능을 정의, CTO 보고를 위해 사용된다.

문제점이 무엇일까?

만약 특정 함수가 다른 함수를 사용 즉, 공유한다고 생각해보자. 재무팀에서 calculatePay 메서드를 수정하였는데,  
이를 reportHours에서 사용한다면? COO(최고운영책임자) 팀은 이를 모르고 사용한다면 문제가 발생할 것이다.
여러 Actor가 해당 코드에 의존하였기 때문에 문제가 발생하는 것이다.  
그렇기 때문에 **서로 다른 액터가 의존하는 코드는 분리해야한다.**

2. 병합

다른 팀에 속한 개발자가 어떠한 요구사항을 받고 각각 Branch를 checkout해서 작업한다고 가정해보자.  
코드가 서로 의존하는 와중에, 서로 다른 요구사항을 받고 작업을 마친후 병합한다면 어떤 일이 발생할까?
우선 Merge 과정에서 Conflict가 발생할 것이다. 이 conflict를 어찌저찌 해결하여 병합한다고 했을 때,  
과연 병합된 코드는 완벽하게 에러가 안나는 상태라고 볼 수 있을까?  
이러한 일을 방지하기 위해서는 **서로 다른 액터에 대한 코드는 분리해야한다.**

### 해결책

데이터와 메서드를 분리해내는 것이 가장 확실한 해결책이다.

아래와 같이 작성한다면 우연한 중복 사례를 피할 수 있다.

```js
class EmployeeData {} // 데이터 구조
class PayCalculator {
  caculatePay() {
    /* 생략 */
  }
} // 메서드
class HourReporter {
  reportHours() {
    const paycaculator = new PayCaculator();
    /* 생략 */
  }
}
class EmployeeSaver {
  saveEmployee() {
    /* 생략 */
  }
}
```

하지만 이를 통해 어떤 작업을 해야할때, 각각의 클래스를 인스턴스화 하기 때문에, 이를 추적하는 것이 어려워 질 수 있다.

이러한 문제를 해결하기 위해서 퍼사드(Facade) 패턴을 사용할 수 있다.

아래와 같은 퍼사드 패턴을 사용하면 메서드에 대한 구체적인 구현은 Employee 클래스에서 담당하지 않고,  
구체적인 구현을 하는 위의 3개의 클래스는 서로를 모르는 상황이기 때문에, 우발적인 중복 상황을 피할 수 있다.

```js
class PayCalculator {
  caculatePay() {
    /* 생략 */
  }
} // 메서드
class HourReporter {
  reportHours() {
    const paycaculator = new PayCaculator();
    /* 생략 */
  }
}
class EmployeeSaver {
  saveEmployee() {
    /* 생략 */
  }
}
// 퍼사드 클래스
class Employee {
  caclulatePay() {
    /* 생략 */
  }
  reportHours() {
    /* 생략 */
  }
  save() {
    const employeeSaver = new EmploteeSaver();
    employeeSaver.saveEmploye();
  }
}
```
