# 함수

함수는 프로그램에서 가장 기본적인 단위이다.

## 작게 만들어라

함수를 만드는 가장 첫번째 원칙은 '작게 만들어라'이다.

함수에서 들여쓰기는 1단이나 2단을 넘어서면 읽기가 어려워진다. 그러니 중첩구조가 깊어지는 함수는 좋지 않다.

## 하나의 기능만 수행하라

**함수는 한 가지 기능만을 수행해야한다**

그렇다면 한 가지 기능의 기준은 무엇인가..??

하나의 추상화 수준에서 하나여야 한다.

의미있는 다른 함수를 추출해낼 수 있다면, 그 함수는 하나의 기능보다 많은 작업을 한다.

## 함수당 추상화 수준은 하나로 만들어라

함수가 한가지 작업만 한다는 것은 함수 내부의 모든 문장의 추상화 수준이 같아야 한다.
하나의 함수 아래에 추상화 수준이 다른 코드를 작성하면, 읽는 사람으로 하여금
특정 코드가 세부사항을 말하는 것인지, 근본 개념을 뜻하는 것인지 알기 어려워진다.

하나의 함수에 아래와 같은 방식으로 작성하는 것은 잘못된 것이다.

```js
render() {
  getHtml();
  const pagePathName = Pathparser.parse(pagepath);
  pagePathName.append("/user");
  /* 생략 */
}
```

getHtml은 추상화 수준이 아주 높지만, 그 이후의 함수호출은 이보다 낮은 추상화 단계의 함수 호출이다.

반면, 아래의 경우를 보면 추상화 단계가 하나이다.

1. 테이트 페이지인지 판단한다.
2. 설정 페이지와 해체 페이지를 넣는다.
3. 페이지를 HTML로 렌더링한다.

```js
renderPageWithSetupsAndTeardown(pageData, isSuite){
  if(isTestable(pagePath)){
    includeSetupsAndTeardownPage(pageData, isSuite);
  }
  return pageData.getHtml();
}
```

코드는 위에서 아래로 향할수록 추상화 수준이 낮은 함수가 위치해야 아래로 내려가면서 읽을 때, 읽기 쉬워진다.

## Switch문

```js
// payroll.js
caclatePay(employee){
  switch(employee.type){
    case COMMISSIONED:
      return calculateCommissionedPay(employee);
    case HOURLY:
      return calculateHourlypay(employee);
    case SALARIED:
      return calculateSalariedPay(employee);
    default:
      /* ... */
  }
}
```

위의 switch문의 문제점은 무엇인가?

1. 새 직원을 추가하면 함수가 더 길어진다.
2. 한가지 이상의 작업을 수행한다.
3. SRP(Single Responsibility Principle, 단일 책임 원칙)을 위배한다.
4. OCP를 위반한다.

이를 해결하기 위해서 추상 팩토리를 만들 수 있다.
