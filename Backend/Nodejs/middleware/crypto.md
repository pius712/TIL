# crypto & hash

## crypto

암호화를 하는 built-in middleware 이다. 이를 통해서 hash를 만들 수도 있고, 일반적인 암호화(복호화)도 가능하다.

### 

## Hash

해쉬는 암호화랑은 엄밀히는 다른 개념이다. 암호화는 키를 통해서 복호화가 가능하지만 해쉬를 통해 만든 값은 복호화가 불가능하다.

### createHash(해쉬 알고리즘)

해쉬 알고리즘에는 sha512, md5, sha1, sha256 등이 있다. md5, sha1은 취약점 발견으로 인해서 안쓰는 것이 좋다.

```js
const crypto = require('crypto');
crypto.createHash('sha512').update('비밀번호').digest('base64');
crypto.createHash('sha256').update('비밀번호2').digest('base64');
crypto.createHash('md5').update('비밀번호3').digest('base64');
```

### update(문자열) 

변환할 문자열을 넣는다. 

### digest(인코딩)

어떤 형식으로 인코딩할 것인지를 인자로 넣어준다. `base64`, `hex` 등이 자주 쓰인다.
