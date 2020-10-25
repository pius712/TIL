php + jQuery -> react + nodejs

Controller/View/Model

## Controller

`---.com/index.php/foo` 가 있으면, 이 foo는 Controller의 foo.php 파일과 일치한다.

클래스로 작성되어 있다. 경로 접속시 클래스의 `index` 메서드 호출한다.
이후 파라미터가 있으면, 예를 들어 `foo/bar`, `bar` 메서드 호출한다.
/파일이름/메서드/파라미터 -> /foo/bar/id

```php
class Foo extends CI_Controller {
  public function index(){
  }
  public function bar($id){
  }
}
```

## View

Controller에서 Echo를 통해서 보내줄 수 있지만, View를 통해서 보내줄 수도 있다.

`$this -> load -> view()` 문법을 통해서

이 파일은 html 모양에 `<?$parameter?>` 와 같은 방식으로 전달할 수 있다.

## Model

데이터와 관련된 부분.
