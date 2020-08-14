# Stack

list methods를 통해서 list를 스택처럼 사용할 수 있다.
statc은 LIFO 방식으로 작동하는데, `append()`와 `pop()` 함수를 사용하면 stack으로 사용할 수 있다.

```py
>>>
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```