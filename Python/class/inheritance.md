# 상속 (inheritance)

## Super Class/ Sub Class

Super Class의 모든 메서드를 Sub Class를 상속하게 된다.  
그리고, 메서드를 추가, 혹은 override할 수 있다.

```py
class Father:
  def hello(self):
    print('Father')

## 상속
class Son(Father):
  def hi(self):
    print('Son')
def main():
  s = Son()
  s.hello()
  s.hi()
main()
>>> Father
>>> Son
```

## 파이썬은 다중상속이 가능하다.

```py
class Father:
  def hello(self):
    print('Father')
class Motehr: 
  def bye(self):
    print('Mother')
## 상속
class Son(Father, Mother):
  def hi(self):
    print('Son')
def main():
  s = Son()
  s.hello()
  s.bye()
  s.hi()

main()
>>> Father
>>> Mother
>>> Son
```

## 오버라이딩

```py
class Father:
  def hello(self):
    print('Father')

## 상속
class Son(Father):
  def hello(self):
    print('Son')
def main():
  s = Son()
  s.hello()
main()
>>> Son
```

## super()

```py
class Father:
  def hello(self):
    print('Father')

## 상속
class Son(Father):
  def hello(self):
    print('Son')
  def hi(self):
    super().hello()

def main():
  s = Son()
  s.hello()
  s.hi()
main()
>>> Son
>>> Father
```

## Constructor 오버라이딩

`__init__` 함수는 오버라이딩을 해줘야한다.  
왜냐하면, super class의 인스턴스 변수를 sub class에서도 사용하게 되는데 인스턴스 변수를 초기화해야하기 때문이다.

```py
class Car:
  def __init__(self, id, fuel):
    self.id = id
    self.fuel = fuel

## 상속
class Suv(Car):
  def __init__(self, id, fuel, size):
    super().__init__(id, fuel)
    self.size = size
```