# mutable/immutable

## mutable

리스트는 mutable 객체이다. 

```python
list = [1,2]
print(id(list))
list += [3,4]
print(id(list))
```

```zsh
4306940384
4306940384
```

튜플은 immutable 객체이다. 즉, + 연산을 하면 새로운 튜플을 만든다. 

```python
tp = (1,2)
print(id(tp))
tp += (3,4)
print(id(tp))
```

```zsh
4410111632
4410090896
```

```python
def add_last(m, n)
  m += n
lst = [1,2]
add_last(lst, [3,4])
>>> lst
[1,2,3,4]

```
```python
def add_last(m, n)
  m += n
# 연산시 m은 새로운 객체를 만들어서 그 주소를 가르치게 된다. 
# tuple은 immutable 객체이기 때문에
tp = (1,2)
add_last(tp, (3,4))
>>> tp
(1,2)

# 해결방법

def add_last(m, n)
  return m+n

tp = (1,2)
tp = add_last(tp, (3,4))
>>> tp
(1,2,3,4)
```