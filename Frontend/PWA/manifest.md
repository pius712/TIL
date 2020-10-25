# web-app-manifest

메인 html 파일 `<head>`에 meta tag 추가.

```HTML
<link rel="manifest" href="manifest.json">
```

manifest.json 파일 생성

## web app manifest generator

- [사이트 링크](https://app-manifest.firebaseapp.com/)

##

### App icon

1. src : 이미지 경로
2. type: 이미지 타입
3. sizes: 이미지 크기

app icons를 지정하지 않을 경우 meta 태그의 icon을 검색한다. `<link rel="icon">`

```json
{
  icons: [{
    "src": "images/../icon.png",
    "type" : "image/png",
    "sizes" : "128x128"
  },{
    "src": ,
    "type" : ,
    "sizes" :
  },{
    "src": ,
    "type" : ,
    "sizes" :
  }]
}
```

### Launch icon

웹 앱이 시작할 때, 거치는 시작 화면을 설정.  
아이콘 + 배경색 + 아이콘 이름

192px 이미지는 지정하는 것이 좋다.

```json
{
  icons: [{
    "src": "images/../icon.png",
    "type" : "image/png",
    "sizes" : "128x128"
  },{
    "src": ,
    "type" : ,
    "sizes" :
  },{
    "src": ,
    "type" : ,
    "sizes" :
  }],
  "background-color": "hex값"
}
```

### Start URL

앱이 시작될 때, 로딩될 페이지를 지정하는 것.

```json
"start_url" : "./"
```

### Display type

앱 화면의 전체적인 모양을 정할 수 있다.

```json
"standalone"
//상단 url 바를 없애서 네이티브 앱처럼 생성 가능
"browser"
// 해당 OS의 웹 브라우저에서 실행
"fullscreen"
//
"minimul-ui"
```

```json
{
  icons: [{
    "src": "images/../icon.png",
    "type" : "image/png",
    "sizes" : "128x128"
  },{
    "src": ,
    "type" : ,
    "sizes" :
  },{
    "src": ,
    "type" : ,
    "sizes" :
  }],
  "background-color": "hex값",
  "start_url" : "./",
  "display" : "standalone"

}
```

### Theme Color

```json
"theme-color" : "hex"
```

### display orientation

```json
"orientation" : "portrait || landscape" (가로 || 세로)
```

### Install banner

## 참고 링크

[Web App Manifest Spec, W3C](https://www.w3.org/TR/appmanifest/)  
[Web App Manifest Spec, MDN](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)  
[Getting Started w/ PWA, Addy](https://addyosmani.com/blog/getting-started-with-progressive-web-apps/)  
[Don’t use iOS meta tags irresponsibly](https://medium.com/@firt/dont-use-ios-web-app-meta-tag-irresponsibly-in-your-progressive-web-apps-85d70f4438cb)  
[Understanding the manifest](https://thishereweb.com/understanding-the-manifest-for-web-app-3f6cd2b853d6)  
[포켓몬 도감 PWA](http://www.pocketjavascript.com/blog/2015/11/23/introducing-pokedex-org)  
[Fullscreen Image](https://www.androidpolice.com/2017/03/23/chrome-beta-58-adds-support-full-screen-progressive-web-apps-minor-ui-changes-tweaks-custom-tabs-apk-download/)
