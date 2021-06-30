# 파이썬의 예외처리

## 예외의 종류

구문 오류 (Syntax Error)

- 프로그램 실행 전에 발생하는 오류

- IDE 도구에서는 자동으로 실행 전에 오류를 체크함

논리적 오류 (Logical Error), 런타임 오류 (Runtime Error)

- 프로그램 실행 중에 발생하는 오류

- 문법적으로 틀린 것이 없어 즉시 인식되지 않지만 의도치 않은 결과를 가져올 수 있음

## 예외 처리

```py
try:
	예외가 발생할 수 있는 코드
except:
	예외가 발생했을때  실행할 코드
else :
	예외가 발생하지 않았을 때 실행할 코드
finally:
	예외 발생 여부와 상관없이 무조건 실행할 코드
```

- 규칙
    - `try` 구문은 단독으로 사용 불가
    - `else` 구문은 반드시 `except` 구문 뒤에 와야 함
- 조합
    - `try` + `except`
    - `try` + `except` + `else`
    - `try` + `except` + `finally`
    - `try` + `except` + `else` + `finally`
    - `try` + `finally`

1. try, except

- 치명적이지 않은 오류지만 프로그램이 멈추는 것을 방지
    > 예외를 그냥 넘어가고 싶은 경우 pass 키워드 사용

```py
def division(a, b):
    x = a / b
    print(x)

# 0으로 나눌 시 예외 발생
# division(4, 0)

try:
    division(4,0)
except:
    print('0으로 나누지 마시오')
# 결과값: 0으로 나누지 마시오

## 2로 나눌 경우
try:
    division(4,2)
except:
    print('0으로 나누지 마시오')
# 결과값: 2.0

## 예외를 변수에 담기
def division(a, b):
    x = a / b
    print(x)

try:
    division(4, 0)

# 예외 객체
except ZeroDivisionError as e:
    print('0으로 나누지 마세요. {0} 에러가 발생 합니다.'.format(e))
```

2. else, finally

- `else`는 예외가 발생하지 않았을 때 실행할 코드 작성

- `finally`는 예외 발생에 관계없이 실행할 코드 작성

```py
def division(a, b):
    x = a / b
    print(x)

try:
    division(4, 0)

# 예외 발생 시 실행
except ZeroDivisionError as e:
    print('0으로 나누지 마세요. {0} 에러가 발생 합니다.'.format(e))

# 예외가 발생하지 않으면 실행
else:
    print('나눗셈을 정상적으로 실행 되었습니다.')

# 예외 상관없이 무조건 실행
finally:
    print('프로그램을 종료 합니다.')
    
# 결과값 : 0으로 나누지 마세요. division by zero 에러가 발생 합니다.
# 결과값 : 프로그램을 종료 합니다.
```

3. raise

- 강제로 예외 발생

- 사용자 정의 클래스를 만들 때
- 아직 구현이 덜 된 코드
- 예외 처리가 필요한 경우

```py
def division():
    x, y = map(int, input('나눗셈의 결과가 1이될 두 숫자를 입력하세요: ').split())
    result = x / y
    if result != 1:

        # 직접 예외를 발생시킴
        raise Exception('나눗셈의 결과가 1이 아닙니다.')
    print(result)

try:
    division()
except Exception as e:
    print('예외 발생:', e)
```

### 예외 객체

예외가 발생하면 예외와 관련된 정보가 생성
> 예외 객체로 활용 가능

```py
a = 0.0

try:
    print(1.0/a)
except ZeroDivisionError as msg:
    print('ZeroDivisionError !!!')
```

### 예외 구분

예외 객체를 활용해 조건문처럼 예외 종류에 따라 코딩을 할 수 있음

```py
num = ['3', 'hi', 2]

try:
    a = input('정수를 입력 : ')
    a = int(a)
    print(a,'번째 요소는 : ',num[a])

except ValueError:
    print('정수를 입력해주세요')

except IndexError:
    print('리스트의 범위를 벗어났습니다')
```

### 예외 구분의 잘못된 예

- 예외 처리의 순서
    > Arithmetic >> ZeroDivision

```py
try:
    print(1/0)
except ArithmeticError:
    print("ArithmeticException occured")
except ZeroDivisionError:
    print("ZeroDivisionError occured")
```