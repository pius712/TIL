# sorting

sorting을 하는 방법에는 여러가지가 있다. 삽입정렬, 버블정렬, 등등...
하지만, 항상 이 정렬 코드를 구현할 필요는 없다. 내장 함수 `sort()` 혹은 `sorted()`함수를 사용하면 된다.

기본적인 내용은 list/sort 문서에도 있다.

## sort

인자는 key, reverse가 있다.  
key는 정렬을 하는 기준을 제시해주는 함수를 넣을 수 있고, reverse는 오름차순, 내림차순 정렬을 정할 수 있다.

- revser=True 내림차순

```py
lst = [3,1,4,2]
lst.sort()
>>> [1,2,3,4]
lst.sort(reverse=True)
>>> [4,3,2,1]
```

- key를 통한 정렬

```py
lst = [('A', 3), ('C', 1),('B', 2)]
# 1번 인덱스의 인자를 통해서 정렬을 한다.
lst.sort(key=lambda x: x[1])
>>> [('C', 1), ('B', 2), ('A', 3)]
# 0번 인덱스의 인자를 통해서 정렬을 한다.
lst.sort(key=lambda x: x[0])
>>> [('A', 3), ('B', 2), ('C', 1)]

lst2 = ['defg', 'hijkl', 'abc', ]
# 길이를 기준으로
lst2.sort(key=len)
>>> ['abc', 'defg', 'hijkl']
```
## sorted(iterable, key, reverse)

리스트의 사본을 만들어 사본을 반환한다. 기존의 리스트는 수정하지 않는다. 
나머지는 같다. 