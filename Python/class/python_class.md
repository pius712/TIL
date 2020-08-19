# 파이썬의 클래스

파이썬의 클래스는 기존의 다른 객체지향언어와 다른 점이 있다. 


```py
class Simple:
  def seti(self, i):
    self.i = i
  def geti(self):
    return self.i
```

객체를 만든다고 해서, 인스턴스 변수가 생성되는 것이 아니다. 

```py
s = Simple()
s.geti()
>>> 에러
```

그렇기 때문에, constructor에서 인스턴스 변수들을 초기화해줘야한다.

```py
class Simple:
  def __init__(self):
    self.i = 0
  ...
```

## 객체에 동적으로 변수, 메서드 추가

```py
class Simple:
  def geti(self):
    return self.i

s = Simple()
s.i = 10
s.geti()
>>> 10
s.hello = lambda: print('hello')
s.hello()
>>> hello
```

## 클래스에 동적으로 변수 추가

```py
class Simple:
  def __init__(self, i):
    self.i = i

Simple.n = 7
Simple.n
>>> 7
```

여기서 Simple을 인스턴스화 시킨다고 하여도, 이 인스턴스는 n 이라는 인스턴스 변수를 가지고 있지 않다.
하지만, `s = Simple()` 을 실행해서 s 인스턴스르 만들고 s.n을 호출하면 7 값이 나온다.  
객체에서 찾았을 때, 해당 변수가 없으면 class에 그 변수가 있는지 찾아보는 것이다.

## 클래스도 객체

파이썬의 클래스는 클래스이자 객체(type class의)이다.  
