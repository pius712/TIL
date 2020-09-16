# Event

- 예시
- 이벤트 버블링, 캡처
  - 이벤트 버블링
  - 이벤트 캡처링
- stopPropagation()
- 이벤트 위임

## 예시 

이번 주제는 자주 마주치지는 않지만, 알지 못하면 해결하기 어려운 문제에 대해서 알아볼 것이다.
Event bubbling과 capture 이 두가지는 같은 이벤트 타입의 2가지 핸들러가 하나의 element에서 활성화될 때, 무엇이 일어나는지를 설명하는 메커니즘이다.  

아래는 이와 관련된 예시 코드이다. 

```js
<button>Display video</button>

<div class="hidden">
  <video>
    <source src="rabbit320.mp4" type="video/mp4">
    <source src="rabbit320.webm" type="video/webm">
    <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
  </video>
</div>
```

<button>이 선택되면, <div> 태그의 class attribute를 hidden에서 showing으로 바꾸어서, <div>비디오가 표시된다.

When the <button> is selected, the video is displayed, by changing the class attribute on the <div> from hidden to showing (the example's CSS contains these two classes, which position the box off the screen and on the screen, respectively):

```js
btn.onclick = function() {
  videoBox.setAttribute('class', 'showing');
}
```
그리고 아래와 같이 두가지의 클릭 이벤트 핸들러를 추가한다.  
첫번째 이벤트 핸들러는 <div> 태그에, 그리고 두번째 핸들러는 <video> 태그에 추가한다.  
이제 비디오 바깥 쪽의 <div> 영역을 클릭하면, 박스는 다시 hidden으로 바뀌고, 비디오 자체가 클릭되면 비디오가 시작이 된다. 

```js
videoBox.onclick = function() {
  videoBox.setAttribute('class', 'hidden');
};

video.onclick = function() {
  video.play();
};
```
하지만 여기서 문제가 생긴다. 비디오를 선택하면 재생이 되는데, 동시에 <di> 태그가 hidden으로 처리되어 버린다.  
이는 video가 <div> 내부에 있기 때문에 발생한다 - div의 일부이다 - . 따라서 video를 선택하는것은 실제로 두가지 핸들러 모두 실행해버리는 것이다. 


## 이벤트 버블링, 캡처

이벤트가 부모 element를 가지는 element에서 발생하게 되면, 모던 브라우저는 2개의 다른 단계를 실행한다.  
capturing phase와 bubbling phase.

### captruing phase  
- 브라우저가 element의 가장 바깥 조상(<html>)에 등록되어 있는 onclick 이벤트 핸들러가 있는지 체크하고, 있다면 실행한다.  
- 그리고 <html> 내부의 그다음 element로 이동하고, 위와 같은 일을 실행하고, 그다음 element ... 이런식으로 실제로 선택된 element에 도달할 때까지 진행한다. 

### bubbling phase

bubbling phase에서는 완전히 반대과정이 발생한다. 

- 브라우저가 선택된 element에 등록되어있는 onclick 이벤트 핸들러가 있는지 체크하고, 있다면 실행한다. 
- 그리고 즉시 조상 element로 가서 위와 같은 동작을 수행하고, <html> element를 만날 때까지 같은 동작을 수행한다. 

모던 브라우저에서는 기본적으로 모든 이벤트 핸들러는 bubbling 방식으로 이벤트 핸들러가 등록이 된다. 따라서, 위의 예시와 같은 경우에는 비디어를 선택하면, <video> element로부터 이벤트 버블이 <html> element까지가게 된다. 

- 브라우저가 video.onclick 핸들러를 찾아서 실행한다. 그러면 비디오가 처음에 시작된다. 
- 그리고 vidoeBox.onclick 핸들러를 찾아서 실행하기 때문에, vidoe가 hidden으로 바뀌어 버린다. 


## stopPropagation()

이것은 꽤나 성가신 동작인데, 이를 `stopPropagation()`을 통해서 고칠 수 있다.  
표준 Event 객체는 `stopPropagation()`이라는 함수를 가지고 있는데, 이는 핸들러의 이벤트 객체가 발생했을 때, 첫번째 핸들러는 실행되고, 이벤트 버블링을 막아줘서 다른 핸들러들이 실행되지 않게 해준다. 

따라서 이전 예시에서의 코드를 아래와 같이 작성해주면 문제가 해결된다. 

```js
video.onclick = function(e) {
  e.stopPropagation();
  video.play();
};
```

---
**Note**
왜 캡처링과 버블링 모두에 신경쓸까? 과거에는 브라우저간에 호환성이 요즘과는 달리 많이 떨어졌었다. 넷스케이프는 이벤트 캡처링만을 사용했고, 인터넷 익스플로러는 이벤트 버블링만을 사용했다. 이후 W3C에서 두개의 방식 모두 표준으로 포함했고, 모든 브라우저는 이 둘 모두를 구현하고 있다. 

**Note**  
언급된 것처럼, 기본적으로 모든 이벤트 핸들러는 버블링 방식으로 등록된다. 그리고 일반적으로 상식적이다. 만약 캡처링 방식을 원하는 경우에는, `addEventListner()` 옵션 값을 통해서 등록이 가능하다. 

---

## Event delegation

Bubbling also allows us to take advantage of event delegation — this concept relies on the fact that if you want some code to run when you select any one of a large number of child elements, you can set the event listener on their parent and have events that happen on them bubble up to their parent rather than having to set the event listener on every child individually. Remember, bubbling involves checking the element the event is fired on for an event handler first, then moving up to the element's parent, etc.

A good example is a series of list items — if you want each one to pop up a message when selected, you can set the click event listener on the parent <ul>, and events will bubble from the list items to the <ul>.

This concept is explained further on David Walsh's blog, with multiple examples — see How JavaScript Event Delegation Works.