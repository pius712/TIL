# Loader

웹팩은 스타일시트, 이미지 등의 일련의 파일들을 모두 모듈로 보고 이를 import한다.
로더는 스타일시트, 이미지, 타입스크립트 등을 자바스크립트에서 로딩할 수 있도록 도와주는 역할을 한다.

```js
module: {
	rules: [
		{
			test: /\.js$/, //정규표현식으로 파일명
			// js 확장자는 아래에 사용할 로더를 사용한다.
			use: [path.resolve('./my-webpack-loader.js')],
		},
	];
}
```

## 자주 사용하는 로더

### css-loader

`npm i css-loader`

```js
module: {
	rules: [
		{
			test: /\.css$/, //정규표현식으로 파일명
			// js 확장자는 아래에 사용할 로더를 사용한다.
			use: ['css-loader'],
		},
	];
}
```

이 경우 style-loader도 같이 사용해야한다.

### style-loader

`npm i style-loader`

```js
use: ['style-loader', 'css-loader'];
```

### file-loader

`npm i file-loader`

```js
{
  test: /\.png$/,
  loader: 'file-loader',
  options: {
    publicPath: './dist/',
    name: '[name].[ext]?[hash]'
  }
}
```

### url-loader
