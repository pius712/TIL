# 깊은복사/ 얕은복사

## 연산자

`==` 내용이 같은가? 
`is` 동일 객체인가? 

```python
r1 = [1,2,3]
r2 = [1,2,3]
>>> r1 is r2 
False
>>> r1 == r2
True

r1 = r2
>>> r1 is r2 
True
>>> r1 == r2
True
```

```python
r1 = ['foo', ('bar', 'boo'), ['far']]
r2 = list(r1)
# 리스트안의 값들은 그 값을 가지고 있는 것이 아니라, 참조값을 가지고 있기 때문에, 복사를 하였을 때 다른 리스트지만 그 안에 있는 값들은 참조값이기 때문에 동일한 객체이다. 즉 'foo' 객체의 참조 값을 저장하고 있고, r2를 만들때, 이 참조값을 복사한다.
>>> r1 is r2
False
>>> r1[0] is r2[0]
True
>>> r1[1] is r2[1]
True
>>> r1[2] is r2[2]
True
```

## 깊은 복사 
참조만을 가져오는게 아니라 값을 전부 복사하는 것이 깊은 복사이다.  
`mutable`의 경우에 얕은 복사를 하고 정보를 수정하면, 참조하는 모든 객체가 영향을 받는다. 따라서, 깊은 복사를 해야할 필요성이 있다.

```python
import copy
r1 = ['foo', ('bar', 'boo'), ['far']]
r2 = copy.deepcopy(r1)
# 새로운 리스트를 만들고, mutable객체는 얕은 복사/ immutable은 깊은복사
>>> r1[0] is r2[0] 
True
>>> r1[1] is r2[1]
True
>>> r1[2] is r2[2]
False
>>> r1 is r2
False
```