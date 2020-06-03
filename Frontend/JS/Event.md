# Event

HTML events are "things" that happen to HTML elements.

When JavaScript is used in HTML pages, JavaScript can "react" on these events.

## HTML Events

HTML 이벤트는 브라우저나 사용자가 하는 어떤 행위가 될 수 있다. 

대표적인 예로는, 
- 웹페이지가 로딩을 끝냈을 때
- input field가 바뀌었을 때
- 버튼이 클릭되었을 때

자바스크립트는 이러한 이벤트가 발생했을 때, 특정 로직을 수행하게 할 수 있다. 

또한, HTML 태그 내부에 `event handler` 속성을 사용할 수 있다.즉, 인라인으로 자바스크립트 코드를 삽입할 수 있다.

```html
<element evnet="doSomething">
```
## Common Events

- onchange: html element가 변경되었을때
- onclick:	유저가 element를 클릭했을때 
- onmouseover:	element에 마우스를 올렸을때
- onmouseout:	element 밖으로 마우스를 빼내었을 때
- onkeydown:	키보드의 키를 눌렀을 때
- onload:	브라우저의 로딩이 끝났을 때
- onsubmit: form이 제출되었을 때

## Event Listener

```js
element.addEventListener(event, function, useCapture);
element.removeEventListener("mousemove", myFunction);
```

The addEventListener() method attaches an event handler to the specified element.

The addEventListener() method attaches an event handler to an element without overwriting existing event handlers.

You can add many event handlers to one element.

You can add many event handlers of the same type to one element, i.e two "click" events.

You can add event listeners to any DOM object not only HTML elements. i.e the window object.

The addEventListener() method makes it easier to control how the event reacts to bubbling.

When using the addEventListener() method, the JavaScript is separated from the HTML markup, for better readability and allows you to add event listeners even when you do not control the HTML markup.

You can easily remove an event listener by using the removeEventListener() method.