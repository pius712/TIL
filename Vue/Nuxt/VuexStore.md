# Vuex store

## fetch 메서드

```js
<script>
export default {
  fetch ({ store, params }) {
    return axios.get('http://my-api/stars')
      .then((res) => {
        store.commit('setStars', res.data)
      })
  }
}
</script>
```

위와 같이 `fetch` 메소드가 있다면, 컴포넌트 로딩 전에 메소드가 먼저 실행된다. 서버사이드 혹은 사용자가 페이지가 이동하기 전에 호출된다.

fetch 메소드는 첫번째 인수로 받은 컨택스트(vuex actions의 context가 아니다)를 사용하여 데이터를 받고, 그 데이터를 스토어에 넣을 수 있습니다. fetch 메소드는 Promise를 리턴한다. Nuxt.js는 컴포넌트가 랜더링 되기 전에 Promise가 종료되기를 기다립니다.