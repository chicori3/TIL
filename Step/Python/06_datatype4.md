# 문자열 자료형의 메소드와 포맷팅

## 문자열 자료형의 특징

문자, 단어 등으로 구성된 문자들의 집합

## 문자열 자료형의 연산

1. 연결 연산자 `+`

2. 반복 연산자 `*`
3. 선택 연산자
4. 범위 선택 연산자

```py
# 연결 연산자
'1' + '2'       # '12'
a = 'Hello '
b = "World"
print(a+b)      # Hello World

# 반복 연산자
'2' * 3         # '222'
'Hi' * 3        # 'HiHiHi'

# 선택 연산자
a = 'Hello'
print(a[0])     # H
print(a[-1])    # O

# 범위 선택 연산자
a = 'Hello'
print(a[1:3])   # el
print(a[0:5:2]) # Hlo

# 역순 정렬
a = 'Hello'
print(a[::-1])  # olleH

# 슬라이싱, 연결
a = '12345'
b = '34567'
c = a[0:3] + b[1:]
print(c)        # 1234567

# 스텝 활용
a = '1,2,3,4,5,6,7,8,9'
print(a[::2])   # 123456789
```

## 문자열 메소드의 종류와 활용법

파이썬의 **문자열 자료형은 변경이 불가능**하기 때문에 직접 문자열을 수정하는 방식이 아닌 변경된 문자를 반환하는 방식으로 메소드를 사용

- `upper()` : 문자열을 대문자로 변경

- `lower()` : 문자열을 소문자로 변경
- `swapcase()` : 대문자는 소문자, 소문자는 대문자로 변경
- `capitalize()` : 첫 문자만 대문자로 변경
- `title()` : 각 단어의 첫 문자를 대문자로 변경
- `strip()` : 문자열 양쪽 끝을 잘라냄
    > 기본은 공백
- `lstrip()`, `rstrip()` : 문자열 왼쪽 끝, 오른쪽 끝을 잘라냄
- `split()` : 문자열을 구분자로 분리해 리스트로 반환
- `splitlines()` : 문자열을 라인 단위로 분리해 리스트로 반환
- `index()` : 해당 문자열의 인덱스를 반환
    > 없는 경우 에러
- `find()` : 해당 문자열의 인덱스를 반환
    > 없는 경우 -1을 반환

## 문자열 포맷팅의 활용

변수를 활용하여 문자열을 생성할 때 사용

1. 중괄호 안에 `format()`의 내용 삽입

```py
a = "{}, World".format("Hello")
print(a)                            # Hello World
```

2. 여러 개를 사용하려면, 순서대로 값을 입력

```py
a = "{} {} {}".format('Hello',', ','World')
print(a)                            # Hello, World
```

3. 중괄호에는 문자열이 아닌 다른 자료형이 올 수 있음

```py
a = "{}, {}, {}, {}".format("2",2,(1,2),[1,2])
print(a)                            # 2, 2, (1,2), [1,2]
```

4. 중괄호에 순서를 적어 포맷팅 출력 순서를 변경 가능

```py
a = "{1} {2} {0}".format("Hello","!","World")
print(a)                            # ! World Hello
```

5. 중괄호에 식별자를 적어 출력 가능

```py
a = "Today is {today}, Tomorrow is {tomorrow}".format(today="Monday",tomorrow="Tuesday")
print(a)                            # Today is Monday, Tomorrow is Tuesday
```

6. 자리 표기 가능
    >   f로 타입을 실수로 변경
    > :0.숫자로 소수점 자리 수 변경
    > :숫자로 공백 출력 가능

```py
a = "{}".format(1/3)                
b = "{:0.2}".format(1/3)            
c = "{:f}".format(3)                
d = "{:3}, {:4}".format(4,10)       
print(a)                            # 0.3333333333333333
print(b)                            # 0.33
print(c)                            # 3.000000
print(d)                            #   4,   10
```