---
title: 예외처리(Exception Handling)
linkTitle: 예외처리
weight: 6
---
### 오류 종류
- Error(에러)
  - 문법적인 오류로 프로그램이 실행되지 않거나 잘못된 결과를 만드는 경우
  - Compile Error: 문법적인 오류로 프로그램이 실행되지 않는 경우 예:17/"0"
  - 논리적 오류: 잘못된 알고리즘으로 잘못된 결과를 만들어 내는 경우
- Exception(예외)
  - 문법적으로는 정상이지만 프로그램 실행 도중에 오류가 발생해서 프로그램이 멈추는 것 예:17/0
  - 개발자가 아무런 행동도 취할 수 없는 예외(메모리부족) 개발자가 처리가 가능한 예외로 나눌 수 있음

### 오류 발생 시 조치
- 컴파일 에러나 논리적 오류는 오류를 수정: 디버깅(프로그램을 부분적으로 수행하면서 메모리를 확인)을 수행
- 예외는 예외 처리를 수행

### 디버깅 방법
- 로깅(logging): 메모리의 값을 직접 출력
- IDE가 제공하는 Debugging Tool 이용
- 테스팅 툴을 이용

### 예외 처리의 용도
- 정상적으로 종료
- 예외 내용 기록
- 예외가 발생했을 때 무시하고 계속 실행하거나 정상적인 값으로 변경해서 계속 실행: 서버

```python
def div(x):
    return 10 / x
try:
    print(div(l1))
    # 0으로 나누어서 예외 발생 - 예외처리를 하지 않았기 때문에 아래 문장을 수행할 수 없음
    print(div(0))
# 예외가 발생했을 때 수행할 코드
except:
    print("예외발생")
print("프로그램 종료 시 수행할 내용")
```

### try ~except 이용한 예외 처리
```python
try:
    예외가 발생할 가능성이 있는 코드
except:
    예외가 발생했을 때 수행할 코드
```
- 발생하는 예외에 따라서 구분해서 처리: except 다음 예외처리 클래스 이름을 기재하고 처리
- 예외처리 클래스 이름을 여러 번 사용하는 경우 위에서부터 순서대로 처리하고 예외처리 구문을 벗어남

```python
li = [10, 20, 30, 40]

# 예외 종류 별로 나누어서 처리
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    print(li[index] / x)
except IndexError as e:
    print(e)
    print(dir(e))
except ZeroDivisionError as e:
    print("0으로 나눈 오류")
```
- 예외 처리 객체를 활용: 예외 처리 클래스 이름 다음에 as 객체를 참조할 이름을 만들어서 사용

### 예외처리 클래스의 계층
- https://docs.python.org/3/library/exceptions.html
- 객체 지향 언어에서는 상위 클래스 타입의 참조형 변수가 하위 클래스 타입의 참조를 저장할 수 있음
- 데이터 타입을 지정하는 언어에서는 이 문법이 중요한데 파이썬이나 자바스크립트처럼 타입을 지정하지 않는 언어에서는 큰 의미는 없음
- 파이썬에서 예외 처리를 할 때 except가 여러 개인 경우 위에 상위 클래스를 배치하면 안됨

```python
li = [10, 20, 30, 40]

# 예외 종류 별로 나누어서 처리
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    print(li[index] / x)

# 모든 예외를 여기(BaseException)서 처리
# 상위 클래스의 참조형 변수에는 하위 클래스 타입의 인스턴스를 대입할 수 있음
except BaseException as e:
    print("1:", e)
except ZeroDivisionError as e:
    print("2:", e)
```
- 상위 클래스 타입의 예외 처리 구문을 위에 작성하면 아래 예외 처리 구문은 호출되지 않음
- 자바 같은 경우 위처럼 작성하면 unreachable code 라고 경고가 발생

### else와 finally
- `except` 다음에 `else`를 사용할 수 있는데 else 블럭은 예외가 발생하지 않은 경우 수행할 구문을 작성
- `finally`는 예외 발생 여부에 상관없이 수행할 구문을 작성

```python
li = [10, 20, 30, 40]

try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    print(li[index] / x)

except ZeroDivisionError as e:
    print("2:", e)
else:
    print("에외가 발생하지 않은 경우 수행")
finally:
    print("예외 발생 여부에 상관없이 수행")
```

### 예외 강제 발생
- 실행 중 문법적으로나 값으로나 예외가 발생한 상황이 아닌데 예외를 강제로 발생
- `raise 예외처리클래스이름(예외 문자열)`
- assertion(단언): 특정 조건을 만족하지 않으면 프로그램을 중단시키는 것
```python
li = [10, 20, 30, 40]

try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    print(li[index] / x)
    # 문법적으로 아무런 문제가 없지만 강제로 예외를 발생 시킴
    if x>=5:
        raise Exception("5보다 큰 수로 나눌 수 없음")
    assert x<5, # 5보다 큰 수로 나눌 수 없음, 강제로 예외를 발생시키는 것과 반대로

except ZeroDivisionError as e:
    print("2:", e)
except Exception as e:
    print(e)
else:
    print("에외가 발생하지 않은 경우 수행")
finally:
    print("예외 발생 여부에 상관없이 수행")
```
- `assert 조건 '예외문자열'`
  - 조건에 맞으면 넘어가고 그렇지 않으면 예외가 발생
```python
li = [10, 20, 30, 40]

try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    print(li[index] / x)
    # 문법적으로 아무런 문제가 없지만 강제로 예외를 발생 시킴
    assert x<5, # 5보다 큰 수로 나눌 수 없음, 강제로 예외를 발생시키는 것과 반대로

except ZeroDivisionError as e:
    print("2:", e)
except Exception as e:
    print(e)
else:
    print("에외가 발생하지 않은 경우 수행")
finally:
    print("예외 발생 여부에 상관없이 수행")
```

### 사용자 정의 예외 클래스
- 사용자가 원하는 메시지를 출력하기 위해서 생성
- 예외에 해당하는 클래스를 상속받아서 `__init__` 메서드를 오버라이딩 한 후 상위 클래스의 `__init__` 메서드에 원하는 문자열을 대입하면 됨

### 예외 처리 구문을 작성하는 경우
- 외부 자원을 사용하는 경우는 반드시 작성하기를 권장
- 파일 핸들링, 네트워크 프로그래밍, 데이터베이스 프로그래밍은 대표적인 외부 자원 사용 서비스임. 이런 서비스를 사용할 때는 상대방 자원이 사용가능한지 예외가 발생했을 때 적절하게 정리를 하는지 여부가 중요
- 예외 처리 구문에 로깅을 하는 것도 중요
  - 어떤 상황에서 예외가 발생했는지를 기록해두면 데이터 분석이나 신입 사원 교육에 도움이 됨

## 파이썬이 제공하는 모듈
### 날짜 및 시간 관련 패키지
- 시간표현방법
  - Timestamp: 1970/01/01 자정을 기준으로 해서 초 단위나 밀리초 단위로 측정한 절대시간
  - UTC, GMT: UTC는 세슘 원자의 진동 수에 의거한 초의 길이
  - LST: 국제 표준시로 UTC를 기준으로 경도 15도마다 1시간 차이를 발생시킨 시간
  - 우리나라는 UTC보다 9시간 빠름, 시간 데이터가 맞게 나오지 않은 경우 9시간 차이가 나면 UTC 설정되어 있는 경우
- struct_time
  - Timestamp가 알아보기 어려워서 실제 사용하는 연, 원, 일, 시, 분, 초로 분할해서 가지는 구조체
- time 모듈
  - `time()`: 타임스탬프 값
  - `sleep(초)`: 현재 스레드를 초 만큼 대기
- datetime 패키지
  - datetime 클래스
  - date 클래스
  - time 클래스
  - timedelta 클래스: 시간 차이
  - tzinfo 클래스: 시간대 정보
- pandas에서 시간 정보를 다룰 때 이 패키지의 클래스들을 사용
```python
# 원하는 날짜를 생성하고 분할해서 사용하고 문자열로 변환한 후 문자열을 가지고 시간을 생성
import datetime

# 현재 시간 생성
dt = datetime.datetime.now()
print(dt)

# 원하는 영역의 시간이나 날짜 가져오기
print("년도: ", dt.year)

# 문자열을 가지고 생성
dt = datetime.datetime.strptime("1987-05-05 12:11", "%Y-%m-%d %H:%M")
print(dt)

# 문자열로 변환
s = dt.strftime("%Y-%m-%d %H:%M")
print(s)

dt1 = datetime.datetime.now()
dt2 = datetime.datetime.strptime("1987-05-05 12:11", "%Y-%m-%d %H:%M")

# 날짜 사이의 빼기는 timedelta 타입
td = dt1 - dt2

print(td.days, td.seconds)
```

### 파일 시스템 관련 패키지
- os.path 패키지: 경로와 관련된 패키지
  - 이 패키지의 메서드들은 경로가 없는 경우 예외를 발생시킴
  - 파일의 존재 여부 그리고 최근 변경 시간 그리고 파일의 크기를 알아내는 메서드를 활용하는 것에 대해서 알아 둘 필요가 있음