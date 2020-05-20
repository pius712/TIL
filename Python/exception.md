# Exception

```python
def main():
  print("hello world")
  try:
    age = int(input("input age: "))
    print("age : ", age)
  except ValueError:
    print("wrong input")
  except ZeroDivisionError:
    print("0으로 나눌 수 없습니다")
  print("nice to meet you")

main()
```

```python
def main():
  foo = 10
  try:
    boo = int(input("number: "))
    print("foo/boo = " , foo/boo)
  except ValueError as mag:
    print(msg)
  except ZeroDivisionError as msg:
    print(msg)
  finally:
    print("프로그램을 종료합니다.")
    # 에러가 발생하든 말든 이 블럭의 코드는 실행이 된다.
main()
```