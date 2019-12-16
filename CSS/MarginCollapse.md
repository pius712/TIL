
# margin collapsing
https://www.opentutorials.org/course/2418/13464
https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing

블록의 top 및 bottom 마진은 때로는 (결합되는 마진 중 크기가) 가장 큰 한 마진으로 결합(combine, 상쇄(collapsed))된다. 

## Adjacent siblings
```HTML
<div style="margin-bottom:20px;"></div>
<div style="margin-top:20px;"></div>
```
이런 식으로 형제간에 마진이 상하로 겹치면 하나만 적용된다. 


## No content separating parent and descendants  

자식 태그의 `margin top`과 부모 태그의 `margin top`을 분리하는 `border`, `padding`, `inline content` 등이 없을 경우에는 마진 겹침 현상이 일어난다. 'margin bottom`의 경우도 마찬가지이다. 겹쳐진 마진(descendants tag)가 부모 태그의 마진 값 보다 커지면 부모 태그를 넘어간다. 
```HTML
 <div id="parent">        
    <div id="child">
        Hello world
    </div>
</div>
```
```CSS
#parent{
  /*border:1px solid tomato;*/
  margin-top:100px;
}
#child{
  background-color: powderblue;
  margin-top:50px;
}
```
![collapse2](../img/collapse2.png)


## Empty blocks
