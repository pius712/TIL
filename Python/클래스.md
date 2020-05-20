# 클래스

## 지역변수/ 전역변수

```python
cnt = 100

def func(n):
  lv = n + 1
  print(lv)
  cnt += 1 


# 여기서 n, lv 는 지역변수
# cnt 는 전역변수
```

```python
cnt = 100
def func():
  cnt = 0
  print(cnt)
# 지역변수 cnt/ 전역변수 cnt가 따로 있다.
>>> func()
0
>>> print(cnt)
100
```

```python
cnt = 100
def func():
  global cnt
  cnt = 0
  print(cnt)

>>> func()
0
>>> print(cnt)
0
```

## class

### 인스턴스 변수

```python
# age라는 인스턴스 변수을 명시하지 않아도 된다. 
class AgeInfo:
  def getter(self):
    return self.age
  def setter(self):
    self.age += 1
```

### 메소드 


### 생성자(constructor, initializer)

```python
class Info:
  def __init__(sef):
    print("new") 
  # 자동으로 호출된다. 

def main():
  o1 = Info()
  o2 = Info()

main()

new~
new~
```

```python
class Info:
  def __init__(self, n1, n2):
    self.n1 = n1
    self.n2 = n2
  def show_data(self):
    print(self.n1, self.n2)
def main():
  o1 = Info(1,2)
  o2 = Info(3,4)
  o1.show_data()
  o2.show_data()    
```
