# String

single quotes와 double quotes 둘 다 String을 나타낸다.

string은 immutable이다. 

'+' 의 경우에는 일반적인 concat이 가능하고, '*' 연산자를 통해서 반복이 가능하다. 또한, 'str1' 'str2' 의 경우 자동으로 str1str2로 concat 

```python
>>> 3 * 'un' + 'ium'
'unununium'
>>> 'Py' 'thon'
'Python'

st = "hello wolrd"
>>> str[0]
h

```
- len 함수 
```python
st = [0,1,2]
>>> len(st)
3

st = "abc"
>>> len(st)
3
```

## method

- lower / upper

```python
foo = 'Pius'
upper = foo.upper()
lower = foo.lower()
```

- strip

```python
foo = ' pius '
foo1 = foo.lstrip()
foo2 = foo.rstrip()
foo3 = foo.strip()
foo1
>>> 'pius `
foo2
>>> ' pius'
foo3
>>> 'pius'
```

- replace

```python
foo = 'pius'
foo1 = foo.replace('us', 'kr')
foo1
>>> pikr
```

- split

```python
foo = "a b c"
foo1 = foo.split(" ")
foo1 
>>> [a, b, c] # list로 반환
```

- find

```python
>>> str =  'what is your name'
>>> str.find("is") # 없는 경우 -1 반환
5
```

- isdigit() / isalpha()

```python
st1 = "123"
st2 = "onetwothree"
st1.isdigit()
>>> True
st2.isdigit()
>>> False

st1.isalpha()
>>> False
st2.isalpha()
>>> True
```

- startwith() / endwith()

```python
str = "pius712"
str.startwith("pi")
>>> True
str.endwith("72")
>>> True
```