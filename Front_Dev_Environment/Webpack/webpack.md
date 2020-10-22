# Webpck

![번들링](../img/wp.png)

## 기본 구조

## Basic Concepts

![overview](../img/webpck.png)

1. Entry
2. Ouput
3. Loader
4. Plugin
5. Resolve

## Entry

## Output

## mode

아래와 같이 3가지 옵션을 넣을 수 있다.

```js
module.exports = {
  mode = "production" || "development" ||  "none"
}
```

## Loader

```js
module.exports = {
  // 생략
  module:{
    rules:[
      {
       test: /\.css$/,
       use: [
           'style-loader',
           'css-loader',
      }
    ]
  }
}
```

## config

- webpack --watch

```javascript
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --watch"
  },
```

- webpack-dev-server

npm i -D webpack-dev-server

```javascript
//package.json
"scripts": {
    "build": "webpack --watch",
    "dev": "webpack-dev-server --hot"
  },
```

```javascript
//webpack.config.js
output:{
        filename : 'app.js',
        path : path.join(__dirname, '/dist'),
        publicPath: '/dist'
    }
```
