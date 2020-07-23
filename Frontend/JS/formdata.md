# Formdata


`FormData` 객체는 key/value 쌍을 XMLHttpRequest, 즉 AJAX를 통해서 보낼 수 있도록 해준다. 
일반적으로 AJAX 기술을 사용할 때는, JSON의 형태로 데이터를 Backend로 보내기 때문에, Form 태그를 통해서 바로 데이터를 전송하지 않는다.  
`FormData`는 form data를 보내기 위해서 만들어졌는데, `form` 태그의 submit() 메서드로 데이터를 보낸 것과 같은 포맷이다. (form tag의 encoding type이 multipart/form-data인 경우에)

- HTTP /POST method
- From Scratch
- Retrieving a FormData object from an HTML form

## Form

form
HTML <form> 요소  
지정된 경우 FormData 객체는 form의 현재 key/value 들로 채워집니다.  
key/value는 submit한 각 요소의 `name` property와 `value`를 사용합니다. 또한 파일 입력 내용을 인코딩합니다.

## HTTP /POST method

그 전에 간단하게, HTTP POST에 대해서 짚고 넘어가자.

HTTP POST method는 data를 서버로 보내는데, request의 body 부분이 Content-Type 헤더에 들어가게 된다. 
A POST request는 일반적으로는 HTML의 form 태그를 통해서 전달된다. content-type은 `<form>` 태그의 `enctype` attirbute나 `<ipnut>`,`<button>` 태그의 `formenctype` attribute를 설정을 해서 정해줄 수 있다. 

- `application/x-www-form-urlencoded`: the keys and values are encoded in key-value tuples separated by '&', with a '=' between the key and the value. Non-alphanumeric characters in both keys and values are percent encoded: this is the reason why this type is not suitable to use with binary data (use multipart/form-data instead)
- `multipart/form-data`: each value is sent as a block of data ("body part"), with a user agent-defined delimiter ("boundary") separating each part. The keys are given in the Content-Disposition header of each part.
- `text/plain`

예시: 

A simple form using the default application/x-www-form-urlencoded content type:
```
POST /test HTTP/1.1
Host: foo.example
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

field1=value1&field2=value2
```

```
A form using the multipart/form-data content type:

POST /test HTTP/1.1 
Host: foo.example
Content-Type: multipart/form-data;boundary="boundary" 

--boundary 
Content-Disposition: form-data; name="field1" 

value1 
--boundary 
Content-Disposition: form-data; name="field2"; filename="example.txt" 

value2
--boundary--
```

## From Scratch


FormData 객체를 만들어서, append() 메서드를 통해서 fields를 추가해 나간다. 

```js
var formData = new FormData();

formData.append("username", "Groucho");
formData.append("accountnum", 123456); // number 123456 is immediately converted to a string "123456"

// HTML file input, chosen by user
formData.append("userfile", fileInputElement.files[0]);

var request = new XMLHttpRequest();
request.open("POST", "http://foo.com/submitform.php");
request.send(formData);
```

**Note**: 
"userfile" 필드는 파일을 보내는 것이다.  
"accountnum"에 할당된 숫자는 FormData.append() 메서드 호출시 바로 문자열로 바뀌게 된다.  
field의 value 부분은 Blob, File, string 어떤 것이든 가능하다. Blob나 File이 아닌 경우 문자열로 전환된다.  

이 예제에서는 FormData 인스턴스가 field의 이름이 "username", "accountnum", "userfile" 으로 가지고 있다. 그리고 XMLHttpRequest method send()를 사용하였다.  

이는 `form` 태그 안의 input의 `name` attribute에 해당 하는 부분이고, 
2번째 인자의 값은 `value` attribute에 해당하는 값이다.   

## Retrieving a FormData object from an HTML form

기존에 있는 form으로부터 data를 받는 FormData 객체를 만들기 위해서는 form element를 명시해야 한다. 

Note: FormData는 input field에서 `name` 속성을 가진 것만을 사용한다. 

`var formData = new FormData(someFormElement);`

예시:
```js
var formElement = document.querySelector("form");
var request = new XMLHttpRequest();
request.open("POST", "submitform.php");
request.send(new FormData(formElement));
```

여기에 추가적으로 데이터를 붙일 수 있다. \

```js
var formElement = document.querySelector("form");
var formData = new FormData(formElement);
var request = new XMLHttpRequest();
request.open("POST", "submitform.php");
formData.append("serialnumber", serialNumber++);
request.send(formData);
```

This lets you augment the form's data before sending it along, to include additional information that's not necessarily user-editable.