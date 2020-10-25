# syntax

## type

### 변수

변수 선언시 `$`를 처음에 붙인다.

문자열 join은 `.`을 통해서 한다.

```php
<html>
  <body>
  <?php
  $a=1;
  echo $a+1; #2
  $first = "hello";
  echo $first." world"; # hello world
  ?>
  </body>
</html>
```

### 상수

```php
<?php
define('TITLE', 'PHP Tutorial'); # 상수 선언
echo TITLE;
define('TITLE', 'JAVA Tutorial'); # 에러 발생
?>
```

### array

## 입출력

`localhost:3030/[path]/[filename].php?id=12345`

```php
<?php
echo $_GET['id'];
?>
```

하면 화면에 화면에 12345가 뜬다.

## include/require

다른 php 파일을 코드 안으로 불러오는 방법

js의 import랑 비슷하다.

`include foo.php` 파일 없으면 warning
`require foo.php` fatal error
