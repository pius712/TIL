# JSON

객체와 배열: 속성의 이름은 반드시 `큰따옴표로 표시된 문자열`. 후행 쉼표는 허용X.

숫자: 선행 0은 허용하지 않습니다. (JSON.stringify()는 선행 0을 무시하지만, JSON.parse()는 구문 오류를 던집니다.) 소수점 뒤에는 적어도 한 자릿수가 뒤따라야 합니다.

## JSON.parse()

`JSON.parse(text[, reviver])`

JSON -> js 객체 으로 만들어 준다.

```javascript
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
// expected output: 42

console.log(obj.result);
// expected output: true
```

## JSON.stringify()

js -> JSON 으로 만들어준다.

## 심화?

json은 js의 object 객체만을 말하는 것이 아니다. 아래의 모든 것이 JSON이 될 수 있다.

```js
JSON = null
    or true or false
    or JSONNumber
    or JSONString
    or JSONObject
    or JSONArray

```

````js
JSON.parse('{}'); // {}
JSON.parse('true'); // true
JSON.parse('"foo"'); // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null'); // null
````
