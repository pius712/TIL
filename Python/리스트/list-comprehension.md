# 컴프리헨션

리스트 컴프리헨션은 list를 만드는 간결한 방식이다.  
일반적으로 새로운 리스트를 만들때, 그 리스트의 값은 다른 iterable에서 특정 연산을 거친 값들을 리스트의 요소로 갖는 경우가 많다. 또는, 다른 리스트에서 특정 조건을 만족하는 요소를 가지고 리스트를 만드는 경우가 많다.



```py
>>> squares = []
>>> for x in range(10):
...     squares.append(x**2)
...
>>> squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

위의 경우 x 변수는 loop가 끝난 이후에도 여전히 남아 있다.  

하지만, 아래와 같이 작성한다면, 이러한 side effects를 없앨 수 있다.

```py
// 람다식 사용
squares = list(map(lambda x: x**2, range(10)))
// 리스트 컴프리헨션
squares = [x**2 for x in range(10)]
```

리스트 컴프리헨션은 `[]` 괄호와 for문 이후의 expression을 포함한다. (for, if 문이 여러개 올 수도 있다.)  
그 결과는 expression을 evaluating한 결과 값이다. 

```py
>>>
>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```
이는 아래의 코드와 같다
```py
>>> combs = []
>>> for x in [1,2,3]:
...     for y in [3,1,4]:
...         if x != y:
...             combs.append((x, y))
...
>>> combs
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

```py
>>> vec = [-4, -2, 0, 2, 4]
>>> # create a new list with the values doubled
>>> [x*2 for x in vec]
[-8, -4, 0, 4, 8]
>>> # filter the list to exclude negative numbers
>>> [x for x in vec if x >= 0]
[0, 2, 4]
>>> # apply a function to all the elements
>>> [abs(x) for x in vec]
[4, 2, 0, 2, 4]
>>> # call a method on each element
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [weapon.strip() for weapon in freshfruit]
['banana', 'loganberry', 'passion fruit']
>>> # create a list of 2-tuples like (number, square)
>>> [(x, x**2) for x in range(6)]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
>>> # tuple은 () 괄호가 붙어야 한다. 그렇지 않으면 에러가 난다
>>> [x, x**2 for x in range(6)]
  File "<stdin>", line 1, in <module>
    [x, x**2 for x in range(6)]
               ^
SyntaxError: invalid syntax
>>> # flatten a list using a listcomp with two 'for'
>>> vec = [[1,2,3], [4,5,6], [7,8,9]]
>>> [num for elem in vec for num in elem]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```]