# Configuring Jest

Jest의 환경설정은 `package.json` 또는 `jest.config.js`에서 가능하다. 

```json
// package.json
{
  "name": "my-project",
  "jest": {
    "verbose": true
  }
}
```

```js
// jest.config.js
// jest.config.js
module.exports = {
  verbose: true,
};
```


## option