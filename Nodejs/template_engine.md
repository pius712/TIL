# template_engine

## raw

`res.sendFile()`을 통해서 html을 보낼 수 있다. 하지만, 변수같은 것을 보낼 수 없기 때문에 템플릿 엔진을 사용한다. 

```javascript
router.get('/', (req,res)=>{
    res.sendFile('html 경로');
})
```

## Pug

### 변수 

아래와 같은 모양의 템플릿 엔진을 사용한다. 들여쓰기가 중요하다.

```pug
doctype html
html
  head
    title= title
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
    block content
```

`-const title = 'express'` 와 같이 js 선언이 가능하다.  
`title=title` 와 같이 = 을 사용해서 변수를 대입할 수 있다.  

```javascript
router.get('/', (req,res)=>{
    res.render('layout'); 
    //laoyout.pug 파일을 렌더링 시킬 수 있다. 
    res.render('layout', {
        title : 'express',
        title2 : 'express2'
    }); 
    // 이렇게 사용하면 layout.pug에 변수 title과 title2도 보낼 수 있다. 
});
```

위 에서 `render()`의 두번째 인자를 통해 보낸 객체를 아래의 pug파일에서 받을 수 있다. 

```Pug
doctype html
html
  head
    title= title1 + ' ' + title2
    // 받은 변수 부분.
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
    block content
```

### selector, attribute

id : `div#pius`  
class : `div.pius`  
attribute: `a(href='www.google.com')`  

```pug
doctype html
html
  head
    title= title
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
    div#pius
    div.pius
    button(type='submit')
    p
        | 여러 라인 사용
        | 여러 라인 사용
        br
        | 태그 삽입
    <p> 여러 라인 사용 여러 라인 사용 <br/> 태그 삽입 </p>
    script. // 스크립트 태그 쓰는 법.
    block content
```
