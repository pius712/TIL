# Footer

Footer를 만들때, 항상 footer가 맨 아래가 아니라 중간에 떠 있는 경우가 생긴다.

왜냐하면, html, body 엘리먼트에 내용이 viewport를 가득 채우지 않을 경우, 그 해당 내용의 height 만큼을 차지하기 때문이다.

이 경우 아래와 같이 내용을 지정해두면, html, body 엘리먼트가 뷰포트를 가득채우게 된다.

```css
html, body {
  height: 100%
}
```

하지만, 이러한 경우에 body 안의 내용이 100%를 넘어서 스크롤이 내려지는 경우 문제가 생긴다. 왜냐하면 html, body는 뷰포트의 100%만을 차지하기 때문에, 아래 스크롤까지 크기를 차지하지 않는다.

이러한 경우 해결책

```css
html, body{
  min-height: 100%;
  height: auto;
}
```
위와 같이 두면, 모든 컨텐츠를 포함하게 된다.

따라서 footer는 아래와 같은 방식으로 붙이면 된다.

```css
.html, body{
  min-height: 100%;
  height: auto;
  position: relative;
}
.footer {
  position : absolute;
  bottom: 0;
}
```