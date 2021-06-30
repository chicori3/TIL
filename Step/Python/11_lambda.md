# 파이썬 함수의 활용과 람다 함수

여러 줄의 코드를 간결하게 표현할 수 있도록 도와주는 함수 정의 방법

- `lambda`로 정의할 수 있다

- 일회성으로 사용할 때 유용

## 람다 함수 정의

1. 람다 함수를 일반 함수처럼 사용
    > 람다 함수는 전통적인 함수와 다른 성격을 지님 (macro)

```py
def add(a,b):
    return a+b
result = add(3,4)
print(result)               # 7

add = lambda a, b:a + b
result = add(3,4)
print(result)               # 7
```

2. 따로 변수에 할당하지 않고 바로 한 줄로 표현 가능

```py
print((lambda a, b: a+b)(3,4))
```

3. def 함수와 같이 기본 매개변수, 키워드 매개변수, 가변 매개변수 설정 가능

```py
print((lambda a, b=1: a+b)(3))          # 4
print((lambda a, b: a+b)(b=1,a=3))      # 4
print((lambda a, *b: a*b)(3,3,4,5))     # 3,4,5,3,4,5,3,4,5
```

4. 조건문과 함께 사용 가능

```py
def func(a,b):
    if a%2==0:
        return a
    else:
        return b
print(func(1,3))

print((lambda a,b: a if a%2==0 else b)(1,3))
```

## 람다 함수 활용

1. `map()` 내장함수와 함께 활용
    > 반복가능한 iterable 객체를 받아서 각 요소에 함수를 적용

```py
# 반복문 사용
def func(x):
    return x*x
a = [1,2,3,4,5]
b = []
for x in a:
    y = func(x)
    b.append(y)
print(b)            # [1,4,9,16,25]

# map() 활용
def func(x):
    return x*x

a = [1,2,3,4,5]
b = map(func,a)
print(type(b))      # <class 'map'>
print(list(b))      # [1,4,9,16,25]

# lambda
print(list(map(lambda x: x*x,[1,2,3,4,5])))
```

2. `filter()` 내장함수와 함께 활용
    > 특정 조건으로 결과값이 참인 요소들을 iterator 객체로 반환

```py
# 반복문 사용
def func(x):
    return x>2

a = [1,2,3,34]
b = []
for x in a:
    if func(x):
        b.append(x)
print(b)

# filter() 활용
def func(x):
    return x>2

a = [1,2,3,34]
b = []
print(list(filter(func,a)))

# lambda
print(list(filter(lambda x: x>2, [1,2,3,34])))
```

3. 복잡한 객체를 정렬할 때 활용

```py
color = [
    ('red', 15),
    ('blue', 16),
    ('black', 10),
]
print(sorted(color))  
print(sorted(color, key=lambda x: x[0]))
print(sorted(color, key=lambda x: x[1]))

# [('black', 10), ('blue', 16), ('red', 15)]
# [('black', 10), ('blue', 16), ('red', 15)]
# [('black', 10), ('red', 15), ('blue', 16)]
```

4. 문자열 포맷팅과 함께 활용

```py
print((lambda x,y : '{}x{}={}'.format(x,y,x*y))(3,4))
```

## 재귀함수

- 자기 자신을 호출하는 함수

- 파이썬은 무한루프에 빠지는 것을 방지하기 위해 일정기간 반복해서 자기 자신을 호출할 경우 오류 발생
    > 종료 조건이 필요함

```py
def recursive(num):
    print(num)
    num +=1
    recursive(num)      # 함수 안에서 자신을 계속 호출함

recursive(1)
```

### 팩토리얼 실습

팩토리얼 : 1부터 n까지의 곱셈의 결과

15 팩토리얼 구하는 함수 작성하기

```py
# 재귀 함수 작성
def factorial(n):
    return n * factorial(n-1)

print(factorial(15))            # 종료 조건이 없어서 에러 발생

# 종료 조건 작성
def factorial(n):
    if n == 0:
        return n * factorial(n-1)

print(factorial(15))

# 람다 함수로 변환
fact = lambda x: x==0 and 1 or x*fact(x-1)
print(fact(15))
```

### 구구단 실습

구구단을 람다 함수, 리스트 내포를 활용해 한 줄로 작성

```py
l = []
for i in range(2,10):
    for j in range(1,10):
        l.append('{}x{}={}'.format(i,j,i*j))
print(l)

# 2단부터 9단까지 구구단 결과를 리스트로 출력
l = []
for i in range(2,10):
    for j in range(1,10):
        l.append(i*j)
print(l)

# 리스트 내포를 활용, 출력문을 한 줄로 작성
print([x * y for x in range(2,10) for y in range(1,10)])

# 두 개의 숫자를 받아 출력시키기
def func(a,b):
    return '{}x{}={}'.format(a,b,a*b)
print(3,4)

print((lambda x,y : '{}x{}={}'.format(x,y,x*y))(3,4))

# 람다 함수와 리스트 내포를 활용해 구구단 출력문 한 줄로 작성
print([(lambda x,y : '{}x{}={}'.format(x,y,x*y) for x in range(2,10) for y in range(1,10)])
```
