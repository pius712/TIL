# Multer

## front

```js
onChangeImages(e) {
  console.log(e.target.files);
  const imageFormData = new FormData();
  [].forEach.call(e.target.files, f => {
    // e.target.files가 유사배열이라서, forEach를 못쓴다. forEach는 인자가 콜백함수.
    imageFormData.append('image', f); { image: [file1, file2] }
  });
  this.$store.dispatch('posts/uploadImages', imageFormData);
},
```

```js
//store/post
actions = {
  uploadImages({ commit }, payload) {
    this.$axios
      .post('http://localhost:8080/post/images', payload, {
        withCredentials: true,
      })
      .then(res => {
        console.log('uploaded');
        commit('concatImagePaths', res.data);
      })
      .catch(() => {});
  }
},
```

```js
mutations = {
	concatImagePaths(state, payload) {
		state.imagePaths = state.imagePaths.concat(payload);
	},
	removeImagePath(state, payload) {
		state.imagePaths.splice(payload, 1);
	},
};
```

```html
<div v-for="(p, i) in imagePaths" :key="i" style="display:inline-block">
	<img :src="`http://localhost:8080/${p}`" style="width: 200px" />
	<div>
		<button type="button" @click="onRemoveImage(i)">
			제거
		</button>
	</div>
</div>
<!-- PostFrom.vue -->
computed: { ...mapState('posts', ['imagePaths']), },
```

## back

```js
// app.js
app.use('/', express.static('uploads'));
```

```js
// routes/post
const upload = multer({
	storage: multer.diskStorage({
		destination(req, file, done) {
			done(null, 'uploads');
		},
		filename(req, file, done) {
			const ext = path.extname(file.originalname);
			// 확장자를 뽑아오는 것.
			const basename = path.basename(file.originalname, ext);
			// pius.png, basename = pius, ext = .png
			done(null, basename + Date.now() + ext);
		},
	}),
	limit: { fileSize: 20 * 1024 * 1024 },
	// 사이즈 제한
});
```

```js
router.post('/images', isLoggedIn, upload.array('image') (req, res) => {
  // console.log(req.files);
  res.send('아하 ㅋㅋ');
});

upload.single //파일 하나
upload.array  // 같은 키로 여러개
upload.fields // 다른 키로 여러개 ?

```

알아서 storage에 저장을 해주고, req.files에 배열 형태로 파일을 저장해준다.
