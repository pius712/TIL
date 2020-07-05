# Grid  

- Grind Container/Item
- 행과 열
- 단위 fr
- repeat 표기법
- Grid Line
- Grid gap(경계 여백)

## Grid Container/Item

바깥 부분의 `wrapper`부분은 Gird Container이다.  
그리고 내부에 있는 아이템들은 Grid Item이다. 

```html
<div class="wrapper">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
  <div>Four</div>
  <div>Five</div>
</div>
```

```css
.wrapper {
  display: grid;
}
```
## 행과 열

그리드의 행과 열은 `grid-template-columns` 및 `grid-template-rows` 프로퍼티로 정의할 수 있다.  
이렇게 하면, 그리드 트랙도 함께 정의된다.

## 그리드 트랙 / 그리드 셀

그리드 트랙은 그리드에 그려진 두 라인 사이의 공간이다. (세로, 가로가 아니라 선 두개 사이에 있는 공간은 트랙이다.) 

그리드 셀은 그리드의 구성 단위이다. 



## 단위 fr

`fr` 단위는 CSS Grid Layout에 도입된 단위로 fraction(분수)의 줄임말이다. 이 단위는 grid container에서 이용 가능한 분수의 공간을 나타내는 것이다.  

이렇게만 보면 이해하기 어렵다. 특정 비율을 차지하는 것인데, 아래의 예시를 보자.

```css
.grid {
  display: grid;
  grid-template-columns: auto 100px 1fr 2fr;
}
```
위의 경우 첫번째 columns는 auto. 즉, 내부의 크기에 따라 결정이된다.  
2번째 column은 100px.
3번째는 남은 크기의 1/3 만큼을 차지하고
4번째는 남은 크기의 2/3 만큼을 차지한다. 

## repeat() 표기법

많은 트랙을 포함하는 커다란 그리드는 repeat() 표기법을 사용하여 트랙의 전체 또는 일부분을 반복해서 나열해 줄 수 있다. 예를 들어 다음과 같이 정의된 그리드의 경우:

```css
.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```
위의 표현은 아래와 같다. 

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

`repeat()` 표기법은 트랙의 목록 중 일부분에만 사용할 수도 있는데, 아래 예제에서는 처음엔 20픽셀 크기의 트랙을 생성하고 다음에 1fr 크기의 트랙을 6번 반복해서 채운 후 마지막에 20픽셀 트랙을 붙여서 그리드를 완성합니다.

```css
.wrapper {
  display: grid;
  grid-template-columns: 20px repeat(6, 1fr) 20px;
}
```

반복 표기법은 트랙의 목록도 함께 나열해서 지정할 수 있는데, 이렇게 하면 트랙의 반복 패턴을 생성해서 사용하게 됩니다. 다음 예제는 그리드가 10개의 트랙으로 구성되어 있으며, 1fr 크기의 트랙 다음에 2fr 크기 트랙이 위치하고, 이 형태가 5회 반복됩니다.

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(5, 1fr 2fr);
}
```
## grid line
[공식문서 참고](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Grid_Layout/Relationship_of_grid_layout)

## grid gap