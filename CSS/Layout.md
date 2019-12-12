# Layout

## Display

HTML 엘리먼트는 모두 Display 속성을 갖는다. 대부분은 `inline` or `block`

### Display 속성의 종류 
* block : 하나의 줄을 가득 채운다. `div` `p` `form` `header` 
* inline : 컨텐츠를 감싼다. `span` `a`
* inline-block : 
* flex :
* none :

## 수평 정렬  
특정 엘리먼트를 중앙 정렬하려면 아래와 같이 코드를 작성하면 된다. 
```html
<div class="center"></div>
```
```CSS 
.center{
    width:1080px;
    margin: 0 auto; /* 아래 위 마진 0 좌우 마진 자동 */ 
}
```
![width](../img/scroll.png)
```CSS
.center {
  max-width: 1080px;
  margin: 0 auto;
}
</style>
```
![max-width](../img/maxwidth.png)
위는 width 아래는 max-width

## box layout 
엘리먼트는 `margin`, `border`, `padding` 와 같은 넓이가 추가로 붙는다. 

```CSS
.class {
  width: 500px;
  padding: 20px;
}
``` 
즉 위와 같은 경우의 엘리먼트는 총 520px를 가지게 된다.   
```CSS
* {
  box-sizing: border-box;
}
```
위와 같이 border-box로 설정을 하면 이전의 엘리먼트는 총 500px를 가지게 되어, `border`, `padding` 의 값을 따로 계산하지 않아도 된다.

## Position

포지션 속성은 엘리먼트가 페이지 어디에 위치할 것인지를 결정하는 속성. 기본 값은 `static`이다.
* `static` : 기본 값.
* `fixed` : 고정된 화면을 기준으로 위치가 지정된다. 페이지가 스크롤, 확대, 축소되어도 같은 위치에 존재한다. 구글의 검색창.  
* `absolute` : 상위의 가장 근접한 엘리먼트를 기준으로 `fixed`와 같이 위치가 설정된다.  position 속성이 `absolute`인 경우 컨테이닝 블록은 `position` 속성 값이 static이 아니고(`fixed`, `absolute`, `relative`,`sticky`) 가장 가까운 조상의 내부 여백 영역이다. 즉. 부모를 계속 찾아간다. static이 아닌 부분까지 찾아간다. 없으면 html까지 올라간다.  
어딘가에 붙이고 싶으면 상위 태그에 position 속성을 고쳐준다.  
* `relative` : 랠러티브(relative)는 top, right, left, bottom과 같은 속성을 주지 않으면 스태틱과 동일하게 위치합니다. 만약 top: -20px; left: 20px과 같은 속성을 주면 위로 20px 왼쪽으로 20px 떨어진 곳에 엘리먼트가 위치하게 됩니다. 이때 생성된 간격은 다음 엘리먼트의 위치에 영향을 주지 않습니다.

```CSS 
.header-search fieldset button{
    /* ...  */
    position: absolute;
    top: 0;
    right: 0;
}
```
![결과](../img/position.png)

```CSS
.header-search fieldset {
    /* ... */
    position: relative;    
}
```

아래와 같이 부모 태그에 relative를 추가해주면 
![결과](../img/relative.png)

* relative 
원래 위치에서 움직인다. 
```CSS
.class {
    position: relative;
    top : -10px;
}
```