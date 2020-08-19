# Sort

파이썬에서 list를 sorting 하는 방법은 크게 두가지가 있다.  
`list.sort()`  `sorted(list)` 이다.

## list.sort()

list.sort() 함수를 하면 원본 list가 정렬이 된다. 

```py
a = [3,2,1]
a.sort()
print(a)
>>> [1,2,3]
```

## sorted(list)

sorted 함수의 경우에는 인자를 list 뿐만 아니라, string, set, tuple 등 다양하게 받을 수 있다.  
대신에 결과값을 list로 만들어 준다. 

```py
a = [3,2,1]
print(sorted(a))
>>> [1,2,3]
print(a)
>>> [3,2,1]
```

```py
# str
sorted("hello")
>>> ["e","h","l","l","o"]

# set
sorted({3,2,1})
>>> [1,2,3]

#tuple
sorted((3,2,1))
>>> [1,2,3]
```