# 파이썬의 함수

## 함수의 정의

입력 값으로 작업을 수행한 뒤 결과 값을 출력하는 것

1. 주로 자주 사용되는 반복된 코드를 일반화하여 함수로 사용
    > 중복된 코드를 줄일 수 있고, 코드의 가독성, 유지보수성을 향상시킬 수 있음
    > 소프트웨어 개발 시 수행 단위로 의미가 있는 코드도 함수로 사용

```py
def sayHello():
    print("Hello")
```

2. 함수의 이름 또한 식별자 규칙을 지켜야 함
3. 제어문과 마찬가지로 콜론과 들여쓰기 주의
4. 아무 행동도 하지 않는 함수는 `pass` 키워드를 적어줘야 함
5. 함수의 설명을 적어둘 수 있음

```py
def Hello():
    "ex"                # 함수 설명
    print("Hello")
```

6. 내장 함수 `help()`를 사용해 해당 함수의 설명을 확인할 수 있음
    > 흔히 사용하는 내장함수들도 help 활용 가능

```py
help(Hello)             # ex
help(len)               # Return the number of items in a container.
```

## 함수의 호출과 반환

함수의 호출 : 정의한 함수명을 불러서 호출

```py
def Hello():
    print("Hello")

Hello()
```

1. 매개변수가 있다면, 해당 인자를 호출할 때 적어줘야 함

```py
def add(a,b):
    print(a+b)

add(1,2)            # 3
add()               # 에러
```

함수의 반환 : 함수 실행 종료 후, 지정한 값을 함수가 호출된 지점으로 반환할 수 있음

```py
def add(a,b):
    print(a+b)

def add2(a,b):
    return a+b

x = add(1,2)
print(x)            # 3 None : 반환할 값이 없다

y = add2(1,2)
print(y)            # 3
```

1. 두 개 이상의 값을 반환하면, 결과 값은 튜플로 반환

2. 매개변수의 자료형은 동적으로 결정되며, 호출되는 순간 해당 인자에 전달되는 객체에 따라 자료형이 결정됨

```py
def func(a,b):
    return a,b

x = func(1,2)
print(x)            # (1, 2)
print(type(x))      # <class 'tuple'>

y = func("문자",['리스트',1])
print(y)            # ('문자', ['리스트', 1])
print(type(y))      # <class 'tuple'>
```

## 지역변수

함수 내에서 만들어진 변수
> 함수가 실행될 때 생성되며, 함수가 종료될 때 사라짐

```py
def func():
    a = 10
    b = 5
    print(a)
a = 20
func()          # func() 함수가 호출될 때 지역변수 a에 10이 할당되고 출력됨
print(a)        # 함수는 종료되고 a를 출력하면 20이 출력됨
print(b)        # 함수가 종료되면 b는 사라지므로 에러
```

## 전역변수

함수 밖에서 만들어진 변수
> 함수와 관계 없이 사용 가능하며, 함수 안에서 참조 가능

```py
a = 10
def func():
    b = 20
    return a+b  # a는 전역변수 b는 지역변수

x = func()
print(x)        # 30
```

1. `global` 키워드를 사용해 함수 안에서 전역변수 활용 가능

```py
a = 10
print(a)        # 10
def func():
    global a
    a = 20
    print(a)

func()          # 전역변수 a의 값이 20으로 변경됨
print(a)        # 20
```

2. 함수의 매개변수로 전달받은 값을 함수 내에서 변경했을 때, 인자로 사용된 호출함수 내에서의 변수의 값은 변경되지 않음
    > 자료형에 따라 다르지만 변경 불가능한 객체인 경우 값을 복사하여 전달

```py
a = 10
print(a)        
def func(b):
    b = 20      # 매개변수 b를 20으로 변경
    print(a)    

func(a)          
print(a)        # 인자로 a를 전달

# 10
# 20
# 10
# a의 값은 변경되지 않음
```

3. 전달 받은 객체 자체의 변경이 아닌 객체의 요소를 변경하는 것은 가능

```py
def func(b):
    b = [1,2,3]
a = [4,5,6]
func(a)
print(a)        # [4,5,6]

def func(b):
    b[1] = 10   # 매개변수 b의 요소를 10으로 변경
a = [4,5,6]     # 전역변수 a는 리스트(변경 가능한 자료형)
func(a)
print(a)        # [4,10,6]
```

## 기본 매개변수

매개변수에 기본값을 설정해 값이 없어도 오류가 발생하지 않음

```py
def func(a,b):
    print(a+b)
func(10,20)         # 30

func(10)            # 에러

def func(a,b=10):
    print(a+b)
func(10)            # 20
```

함수 생성 및 호출 시 기본값이 있는 매개변수가 일반 매개변수보다 앞에 올 수 없음

```py
def func(a=10,b):
    print(a+b)
func(10,20)         # 에러
```
## 키워드 매개변수

1. 함수를 호출할 때 인자는 순서대로 전달됨

```py
def func(a,b,c,d,e):
    print(a+b-c-d+e)
func(1,2,3,4,5)       # 1
func(5,4,3,2,1)       # 5
```

2. 순서와 상관없이 매개변수의 이름과 함께 값을 전달할 수 있음

```py
def func(a,b,c,d,e):
    print(a+b-c-d+e)
func(a=1,b=2,c=3,d=4,e=5)   # 1
func(e=5,d=4,c=3,b=2,a=1)   # 1
```

## 가변 매개변수

1. 일반 매개변수 다음에, *매개변수로 가변 인자를 전달할 수 있음

2. 일반 매개변수에 할당되는 인자를 제외한 나머지 인자는 튜플로 할당

```py
def func(a, *arg):
    print(a, arg)

func(1)             # 1 ()
func(2,3)           # 2 (3,)
func(2,3,4,5,6)     # 2 (3,4,5,6)
```