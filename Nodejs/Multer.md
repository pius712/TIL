# Multer

```js
const upload = multer({
  storage: multer.diskStorage({
    destination(req, file, done) {
      done(null, 'uploads');
    },
    filename(req, file, done) {
      const ext = path.extname(file.originalname);
      // 확장자를 뽑아오는 것.
      const basename = path.basename(file.originalname, ext); // pius.png, basename = pius, ext = .png
      done(null, basename + Date.now() + ext);
    },
  }),
  limit: { fileSize: 20 * 1024 * 1024 }, // 사이즈 제한
});
```

```js
router.post('/images', isLoggedIn, upload.array('image') (req, res) => {
  res.send('아하 ㅋㅋ');
});

upload.single //파일 하나
upload.array  // 같은 키로 여러개
upload.fields // 다른 키로 여러개 ?

```
