# AJAX 

## 객체 생성 

```javascript 
var xhttp = new XMLHttpRequest();
```

## request

### GET / POST 

- GET 

```javascript
xhttp.open("GET", "demo_get.asp", true);
xhttp.send();
```
- POST 

```javascript
xhttp.open("POST", "ajax_test.asp", true);
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhttp.send("fname=Henry&lname=Ford");
```

### Request

onreadystatechange  
XMLHttpRequest 객체 내에 함수로써, request의 response를 받았을 경우에 실행될 코드를 적는다. 

```javascript
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    document.getElementById("demo").innerHTML = this.responseText;
  }
};
```

### Response


### 코드 분석하기 

```javascript
var xhr = new XMLHttpRequest(); // 객체 생성
xhr.onload = function () {
    if (xhr.status === 201) {
    console.log(xhr.responseText);
    getUser();
    } else {
    console.error(xhr.responseText);
    }
};
// 응답을 받았을 경우에, statuscode가 201이면 실행. 아니면 error실행
xhr.open('POST', '/users');
xhr.setRequestHeader('Content-Type', 'application/json');
xhr.send(JSON.stringify({ name: name })); 
//post로 /users에 request를 보내고, header에 타입 명시.  
```
