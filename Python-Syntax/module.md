# module

## 모듈 전체

```python
#circle.py
def foo():
  print("hello")
```

```python
import circle

def main():
  circle.foo()
```

## 함수 단위로

```python
#circle.py
def foo_a():
  print("foo_a")

def foo_b():
  print("foo_b")
```

```python
from circle import foo_a
from circle import foo_b as foo_c

def main():
  foo_a()
  foo_c()
```

## built-in 함수/모듈

### 함수 

- print()
- input()


### 모듈

- math

```python
import math

math.fabs(-10)
# math.cos / sin ...
```