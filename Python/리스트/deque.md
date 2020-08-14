# Queue

Using Lists as Queues

list에서 첫 인덱스에 인자를 insert, pop 하는 것은, 비효율적이다. (인자들을 한칸씩 옮겨줘야하기 때문)

그래서 , `collections.deque`를 사용하면 queue를 사용할 수 있다. 

```py
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```