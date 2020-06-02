# Cookie

## Read

```js
allCookies = document.cookie;
```

위의 allCookies는 `;` 으로 구분되는 key value 형태의 모든 쿠키 리스트를 가지는 string이다. 

## Write

```js
document.cookie = newCookie;
```

위의 쿠키는 `key=value` 형태의 string인 newCookie를 저장하는 코드이다. 

```js
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";
```
위는 쿠키에 expire을 추가한 것.

## 간단한 사용법

```js
document.cookie = "name=oeschger";
document.cookie = "favorite_food=tripe";
function logCookie() {
  console.log(document.cookie);
}
logCookie();
```

```zsh
name=oeschger; favorite_food=tripe; 
```

