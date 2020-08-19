# str

텍스트 데이터는 str 객체로 다루어진다. Strings는 immutable sequences of Unicode code points이다. 

파이썬 문자열은 변경할 수 없다.(immutable, 불변)  
그래서 문자열의 인덱스로 참조한 위치에 대입하려고 하면 에러가 난다:

```py
>>> word[0] = 'J'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> word[2:] = 'py'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

## str object

파이썬은 애초에 모든것이 객체이다. 숫자, 문자열, 함수 등...
그런데 comparison 연산자에 `==`, `is`는 어떻게 써야하는가? 라는 의문이 생긴다.

`==` 연산자는 내용이 같은지를 비교하는 연산자이고, `is` 는 같은 객체인가?를 비교하는 연산자이다.
그런데...
```py
a = "hello"
b = "hello"
print(a is b)
>>> True
print(a == b)
>>> True
```
위와 같은 결과가 나온다. 이는 `object interning`과 관련된 내용이다.
초기화된 string을 메모리에 저장할때, 메모리에 있는 어떤 문자열과 같은 문자열을 만드려고 하면, 메모리에 새로운 공간을 할당하는 것이 아닌,  메모리에 저장되어 있는 string 객체를 참조한다. 
문자열의 경우 20자 미만의 공백 미포함 문자열에 대해 interning을 한다.

## split(sep=None, maxsplit=-1) 함수

알고리즘 문제를 풀다보면 split() 함수를 많이 사용하게 된다. [백준1152 문제](https://www.acmicpc.net/problem/1152)를 풀면서 이상한 점을 발견. ` Mazatneunde Wae Teullyeoyo` 문자열을 `split()` 하면 ['Mazatneunde', 'Wae', 'Teullyeoyo']와 같이 생성된다. 앞의 공백을 무시해버린다.

아래는 공식 문서

sep을 delimiter로 사용하여서 문자열을 단어의 리스트로 만들어 반환한다.  
만약 maxsplit 인자가 있다면, 최대 maxsplit 만큼의 split만 하게 된다. 

sep 인자가 제공된다면, 연속된 delimiter가 그룹지어지지 않으면, 빈 문자열로 나누는 것으로 간주한다. 예를들어 '1,,2'.split(',')가 있으면 결과는 ['1', '', '2']가 된다.  
sep 인자는 여러개의 charater일 수도 있다. '1<>2<>3'.split('<>') returns ['1', '2', '3']) 

빈문자열을 어떤 sep인자로 splitting하면, returns [''].

For example:

```py
>>>
>>> '1,2,3'.split(',')
['1', '2', '3']
>>> '1,2,3'.split(',', maxsplit=1)
['1', '2,3']
>>> '1,2,,3,'.split(',')
['1', '2', '', '3', '']
```

---
**note**

sep이 명시되지 않으면, 다른 splitting 알고리즘이 실행된다.  
연속된 whitespace는 single separator로 간주되고, 그리고 그 결과값은 만약, 나누어질 string이 맨 앞과 맨 뒤에 띄어쓰기가 있다면, 빈 문자열을 가지지 않는다. 
해석 => `'   1   2   3   '.split()` 의 경우에는 1 앞의 연속된 띄어쓰기는 단일한 separator로 간주되기 때문에, 빈칸 전체가 하나의 separator이다. 

결과적으로, 빈 문자열 또는 띄어쓰기만으로 구성된 string은 split한 결과가 `[]`이다. 

---

For example:
```py
>>>
>>> '1 2 3'.split()
['1', '2', '3']
>>> '1 2 3'.split(maxsplit=1)
['1', '2 3']
>>> '   1   2   3   '.split()
['1', '2', '3']
```