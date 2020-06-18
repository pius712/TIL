# default parameter

```js
function sayHello(name = 'pius'){
  return name;
}
sayHello(); 
>>> pius
```

```js
const sayHello = (name = 'pius') => name;
sayHello(); 
>>> pius
```