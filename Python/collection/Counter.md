# Counter

## Counter object

Counter은 hashable objects를 카운팅하기 위한 dict의 subclass이다.  
이는 unordered collection으로 원소들이 dictionary key로 정렬되어 있다. 그리고 그들의 카운트가 dictionary의 value로 있다.  

원소들은 iterable 객체로 부터 counted 될 수 있다. 또는 맵핑 가능한 객체로 부터 초기화 될 수 있다.

```py
>>> # Tally occurrences of words in a list
>>> cnt = Counter()
>>> for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
...     cnt[word] += 1
>>> cnt
Counter({'blue': 3, 'red': 2, 'green': 1})
```

```py
>>> c = Counter()                           # a new, empty counter
>>> c = Counter('gallahad')                 # a new counter from an iterable
>>> c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
>>> c = Counter(cats=4, dogs=8)             # a new counter from keyword args
```