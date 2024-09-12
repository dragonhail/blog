---
title: Function
linkTitle: Function
weight: 2
---
- 한 번에 실행되어야 하는 문장들을 하나의 이름으로 묶어서 독립적으로 실행할 수 있도록 해주는 개체
- 파이썬에 메모리 할당의 최소 단위
- 함수 안에서 생성한 데이터는 함수 안에서만 사용이 가능
- 함수를 정의하고 함수 이름을 호출하면 함수가 저장된 곳의 참조를 호출하고 함수의 내용을 수행하고자 할 때는 함수이름() 의 형태여야 함
- 함수 사용 이용 이유
  - 모듈화: 프로그램을 기능 단위로 분할해서 수행
  - 반복 사용: 자주 사용하는 문장을 매번 작성하는 것이 아니고 한 번 만들어두고 호출만으로 사용
- 함수의 종류
  - built in function: 언어가 제공해주는 함수
  - User Define Function(사용자 정의 함수)
    - 3rd party function: 자주 사용할 것 같은 함수를 다른 개발자가 만들어서 제공
- 파이썬에서 함수는 일급객체
  - 함수도 하나의 자료형
  - 실행 중에 함수를 생성하는 것이 가능
  - 변수에 함수를 대입 가능
  - 함수의 매개변수로 함수를 사용하는 것 가능
  - 함수의 결과로 리턴하는 것 가능

### 함수의 호출
- 함수를 정의하면 static 한 메모리 영역에 함수가 저장되고 함수를 호출하면 이 영역의 내용을 기반으로 stack 이라는 임시 메모리 영역을 할당해서 함수를 수행하고 함수의 수행이 종료되거나 return 을 만나면 return 되는 데이터를 가지고 호출한 곳으로 돌아감
- 이 때 자신이 만든 stack은 소멸
- stack: 임시영역, 함수가 주인, 크기제한 있음(1MB)
- heap: 영구적영역, 프로그램이 주인, 크기 무제한(2^64)
  - static영역: 쓰기와 읽기만 가능, 수정과 삭제 안됨, 상수와 정의(함수, 클래스)
  - Instance영역: 모든게 가능한 영역
- 프로그램 만들면 메인스택 생성
- 리눅스 `rm`: 하드링크 수 1 감소시키는 명령, 하드링크 수 0가 되면 삭제, 파일은 기본 하드링크 수가 1
  - 파이썬도 레퍼런스 카운터를 이용, 지울 때 마다 레퍼런크카운트1감소, 0이되면 메모리영역소멸

### built in function
- 프로그래밍 언어가 제공하는 함수
- 확인: https://docs.python.org/3/library/functions.html
- 코드로 확인: dir(\_\_builtins__)
- 이 함수들은 별도의 import 없이 사용 가능

### 고전적인 함수의 정의
```python
def 함수이름(매개변수나열):
    함수내용작성
    [return 데이터]
```
### 함수 호출
- 함수이름 -> 함수의 참조를 리턴
- 함수이름() -> 함수를 호출해서 실행
```python
# 매개변수도 없고 리턴도 없는 함수
def noArgNoReturnFunc() -> None:
    print("매개변수가 없고 리턴도 없는 함수")
    return None

# 함수 이름만 호출하면 참조가 리턴
print(noArgNoReturnFunc)

# 함수 호출
noArgNoReturnFunc()
```
- return이 없는 함수를 만들면 함수의 수행이 종료되면 이 함수의 결과는 다른 곳에서 사용을 못함
- 실제 함수들은 print 하는 경우가 드물기 때문에 return 이 없는 함수는 대부분 매개변수의 데이터에 조작을 가하는 함수일 가능성이 높음

### 매개변수
- 함수를 호출할 때 넘겨주는 데이터
- 매개변수는 함수를 호출할 때
```python
# 매개변수가 있는 경우와 없는 경우
def noArgFunc() -> None:
    for _ in range(3):
        print("매개변수가 없는 함수")

# 파이썬에서도 매개변수에 자료형을 기재해주는 것을 권장
def argFunc(n: int) -> None:
    for _ in range(n):
        print("매개변수가 있는 함수")
```
- 매개변수의 자료형에 따라서 매개변수를 이용해서 원본의 데이터를 변경할 수 있고 그렇지 않을 수도 있음<br>
예전에는 call by value, call by name 등으로 분류를 했음<br>
파이썬에서 하나의 자료형을 의미하는 byte, int, float, complex는 참조가 아니라 값을 넘겨주는 구조로 동작을 하고 나머지 자료형은 참조를 넘기는 형태로 동작을 함<br>
하나의 데이터를 넘겨주면 함수 내부에서 값을 변경하더라도 함수 외부의 데이터는 변경되지 않으며 여러 개의 데이터를 묶어서 넘기는 경우 함수 내부에서 요소의 값을 변경하면 외부의 데이터도 변경이 적용<br>
함수의 매개변수로 데이터 묶음을 전달할 때는 함수의 설명이나 return 타입을 잘 확인해봐야 함
```python
# 하나의 값을 매개변수로 받아서 값을 변경하는 함수
def callByValue(n:int) -> None:
    print("n:", n)
    n = 10
    print(f"함수 내부에서 수정한 후 n:{n}")

x = 20
print(f"함수 호출 전: x: {x}")
# 함수에게 하나의 값을 전달하는 경우는 함수 내부에서 데이터를 수정할 수 없음
callByValue(x)
print(f"함수 호출 후 x:{x}")

def callByReference(li:list) -> None:
    print(f"함수 내부의 li: {li}")
    li[0] = "joy"
    print(f"함수 내부에서 수정한 후 li:{li}")

espa=["조이", "karina"]
print(f"함수 호출 전의 espa:{espa}")
# 벡터 자료형을 넘기는 경우는 함수 내부에서 벡터 자료형의 요소를 변경하면 변경된 함수 외부의 데이터에 적용됨
# 벡터 자료형의 경우는 참조를 넘기기 때문
callByReference(espa)
print(f"함수 호출 후의 espa: {espa}")
```
- 파이썬은 매개변수를 내부에서 dict로 처리
  - C언어나 자바는 매개변수를 배열로 처리, 함수 호출할 때 매개변수의 순서를 변경할 수 없음
  - 기본적으로는 순서대로 매개변수를 대입해야 하지만 순서를 변경해서 이름을 가지고 대입해도 됨
```python
def orderParameter(a: int, b: int) -> None:
    print(a)
    print(b)
orderParameter(10, 20)

# 파이썬에서는 매개변수에 데이터를 대입할 때 이름과 함께 대입하는 것이 가능
# 순서를 변경해도 됨
# 이름을 생략하면 순서대로 대입함
orderParameter(a=10, b=30)
orderParameter(b=30, a=10)

# 매개변수에 이름을 대입할 때 한번 이름을 대입하면 그 이후 모든 데이터에 이름을 대입해야 함
# 첫번째 매개변수는 함수를 수행하기 위한 가장 중요한 데이터를 배정해서 이 데이터의 경우는 이름을 입력하지 않고 입력하도록 하는 경우가 많음
orderParameter(a=200, 100) # 실행안됨
orderParameter(100, b=100)
```
- 매개변수에 기본값 설정 가능
  - 매개변수의 데이터는 함수를 호출할 때 반드시 넘겨주어야 하지만 기본값을 설정하면 넘겨주지 않아도 됨
  - 매개변수 생략이 가능

```python
# 매개변수에 기본값이 있는 경우 함수를 호출할 때 생략하고 대입하는 것이 가능
# 매개변수에 기본값을 설정하면 뒤에 오는 모든 매개변수에도 기본값을 설정해야 함
def defaultParameter(a:int, b:int=0 c:int=0) -> None:
    print(a)
    print(b)

defaultParameter(10)

# range(1, 10, step=1)
r = range(stop=10, start=1, stop=2)
print(r)
```

### 함수의 리턴을 만들 때 여러개의 값을 한꺼번에 리턴 가능
- 여러 개의 값을 하나의 tuple로 만들어서 리턴
- 파이썬은 튜플의 데이터를 분해해서 할당하는 것이 가능하기 때문에 이런 데이터를 여러 개의 변수에 할당할 수 있음
```python
# 여러 개의 데이터 리턴하면 튜플로 묶어서 리턴
def tupleReturn() -> tuple:
    return 100, 200

result = tupleReturn()
print(type(result))

r1, r2 = tupleReturn()
```
### 순수 함수와 비순수 함수
- pure function(순수 함수)
  - 함수의 실행이 외부 상태에 영향을 끼치지 않는 함수: 매개변수를 받아서 수정했을 때 외부의 데이터에 영향이 없어야 함
  - 입력 값이 같으면 언제나 동일한 출력을 만들어내는 함수: 랜덤같은 값을 사용하지 않아야 함
- impure function(비순수 함수)
  - 함수의 실행이 외부에 데이터에 영향을 주는 경우
  - 동일한 입력을 가지고 다른 출력을 만들어내는 함수

### 매개변수의 unpacking
- list나 tuple 그리고 set의 unpacking
  - 매개변수를 대입할 때 * 과 함께 3가지 데이터를 대입하면 순서대로 분할해서 대입이 됨
  - dict의 경우는 * 과 함께 대입을 하게 되면 *key*가 순서대로 대입됨
- dict의 경우 **과 함께 입력하면 동일한 이름의 매개변수에 key의 *값*이 전달됨
  - 그래프 그리는 함수에서 많이 사용
  - 그래프의 경우는 옵션의 종류가 많고 각 옵션의 기본값이 많기 때문에 dict로 필요한 매개변수만 넘겨서 사용을 하도록 만드는 경우가 많음

```python
# 매개변수가 여러 개일 경우 1개로 대입해서 분할해서 적용
def personalInfo(name:str, age:int, gender:bool) -> None:
    print(f"이름: {name}")
    print(f"나이: {age}")
    print(f"성별: {gender}")

# personalInfo("아담", 34, True)
# personalInfo(name="아담", gender=False, age=32)

# 여러 개의 매개변수에 값을 대입할 때 list, tuple, set 1개를 사용할 수 있는데 이 경우는 앞에 *를 추가해야 함
personalInfo(*["아담", 34, True])

# dict는 *를 설정하면 key가 순서대로 대입됨
personalInfo(*{"name":"아담", "age":34, "gender":True})

# dict는 **을 설정해야 value가 대입됨
# 변수 이름과 동일한 key의 값이 대입됨
personalInfo(**{"name":"아담", "age":34, "gender":True})
```

### 가변 매개변수
- *을 이용해서 매개변수를 설정하면 매개변수의 개수에 상관없이 대입이 가능
- *을 이용해서 매개변수를 설정하면 데이터는 tuple이 됨
- **을 이용해서 설정하면 데이터는 dict로 묶임
  - 매개변수 앞의 데이터는 이름과 함께 대입이 안됨
```python
# help(max)
print(max(10,30,20,40)) # 매개변수 개수 상관없음

# 매개변수를 만들 때 **를 이용하면 dict로 데이터가 대입
def dictFunction(** args) -> None:
    for i in args:
        print(i)
dictFunction(name="adam", age=21, gender=False)
```

### 함수를 정의할 때 매개변수나 리턴 타입에 애너테이션 추가 가능
- 매개변수를 만들 때: 다음에 문자열을 추가하는 것이 가능
- 리턴할 때는 ) 와 : 사이에 설명을 추가 가능
```python
# : 다음에 표현식을 설정해서 값의 제한을 설정할 수 있음
def annotationFunc(score: "int>=0" = 0) -> None:
    print(f"정수:{score}")
```

### 도움말 설정
- 함수도 하나의 자료형(객체), 일급객체(속성을 가질 수 있음)
- 함수에 도움말을 추가하는 방법
  - 함수 상단에 '''나 """로 문자열을 만들어서 감싸는 형식
- \_\_doc__ 속성에 문자열을 대입하는 방식
  - 도움말을 작성하면 help에 보여지게 됨

```python
def annotationFunc(score: "int>=0" = 0) -> None:
    print(f"정수:{score}")
annotationFunc.__doc__ = "함수의 속성으로 도움말 추가"
help(annotationFunc)
```

### 함수의 내장 속성
- \_\_name__: 함수의 이름
- \_\_default__: 기본 인수값
- \_\_code__: 코드 객체
- \_\_globals__: 함수의 전역 영역

### 함수는 일급 객체
- 일급 객체의 조건
  - 하나의 자료형으로 취급
- 일급 함수
  - 함수를 실행 중에 생성할 수 있어야 함
  - 파이썬에서는 함수 안에서 함수를 생성가능하고 lamda를 이용해서 생성이 가능하기 때문에 파이썬의 함수는 일급 함수
- 함수를 변수에 대입
  - 실제적으로 사용되는 경우는 드물고 함수가 함수를 리턴하는 경우 사용
- 함수를 매개변수로 받는 것이 가능
```python
def plus(a, b):
    return a+b

def mins(a, b):
    return a-b

def calc(f, a, b):
    return f(a, b)

print(calc(plus, 20, 20))
```
- higher-order function(고위함수)
  - 함수가 함수를 리턴
  - 이 문법을 이용해서 함수 내부의 데이터를 함수 외부에서 수정이 가능