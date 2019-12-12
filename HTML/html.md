# HTML

웹 페이지에서 html 문서만 보려면 
```javascript
document.head.parentNode.removeChild(document.head);
```
를 통해서 head 부분을 날리면 head에 있는 css도 날아간다. 

## 태그
* 관계  
```html
<parent>
    <chilrdren>     
    </chilrdren>
</parent>
```

* heading 태그  
중요도 순서대로 일종의 머릿말 역할을 하는 것.  
chrome 확장 프로그램의 headingsMap 받으면 순위대로 볼 수 있다. 
```html
    <h1>네이버</h1>
    <h2>로그인</h2>
    <h3>급상승 검색어</h3>
```

* a 태그 
href 속성을 통해서 링크를 걸어줄 수 있다. 
```html
    <a href="https://www.naver.com" >네이버</a>
```

* fieldset, legend 
```html
<fieldset>
    <legend>검색</legend>
</fieldset>
```

* input
```html
<input type="checkbox"/> // 여러가지 체크가능 
<input type= "radio" /> // 다중택일  
<input type="text" /> //text 
<input type="password" /> //password 

* button
```html
<button></button>
```


* img tag

```html
<img src = "./경로" alt="부가설명"> 
```

* i tag  
    1. 기울임 태그
    2. 아이콘 태그 

### 이미지 스프라이트


