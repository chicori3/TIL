# 파이썬의 조건문

## 불(Bool) 자료형

참과 거짓을 나타내는 자료형

- 오직 **참과 거짓** 두 값만 가질 수 있음
- 파이썬은 대소문자를 구별하기 때문에 **True, False**로 정확히 사용해야 함

1. 내장 함수 `bool()`을 활용해 참과 거짓을 확인할 수 있음

```py
# 문자열
print(bool("abc"))      # True
print(bool(""))         # False

# 숫자
print(bool(1))          # True
print(bool(0))          # False

# 리스트
print(bool([1,2]))      # True
print(bool([]))         # False

# 튜플
print(bool((1,2)))      # True
print(bool(()))         # False

# 사전
print(bool({'a':1}))    # True
print(bool({}))         # False
```

## 관계 연산자(비교 연산자)

관계 연산자는 bool 값을 반환

```py
print(1==1)             # True
print(1==2)             # False
print(1>0)              # True
print(1>=1)             # True
print(1!=1)             # False
```

## 논리 연산자

논리 값을 판단해주는 연산자로 and, or, not 세 가지가 있음

## 연산자 활용

1. 관계 연산자와 논리 연산자를 함께 사용하는 경우가 많음

```py
a = 1
b = 2

print(a > 0 and b > 1)      # True
print(a == 0 or b != 1)     # True
```

2. and, or 연산자의 출력
    > and 연산자 : 둘 다 True일 때만 True, 오른쪽 출력
    > or 연산자 : 둘 중 하나만 True여도 True, 왼쪽 우선 출력

```py
print("a" and "b")          # b
print("a" or "b")           # a
```

## 조건문의 정의

프로그램의 실행을 제어하기 위한 제어문 중 하나로 조건에 따라 실행 결과를 다르게 할 수 있음
> 콜론, 들여쓰기 필수

```py
if(True):
    print(1)    # 1
print(2)        # 2

if(False):
    print(1)    # False 이므로 출력 X
print(2)        # 2
```

## 조건문의 종류와 특징

1. if else 조건문
    > if와 else는 같은 레벨

```py
a = 2
if(a==1):
    print(1)
else:
    print(2)    # 2
```

2. if else if 조건문
    > elif를 활용해 여러 개의 조건 추가 가능
    > 조건이 같지 않도록 주의

```py
a = 2
if(a==1):
    print(1)
elif(a==2):
    print(2)
elif(a==3):
    print(3)
else:
    print(4)    # 2
```

3. 중첩 조건문

```py
a = 1
b = 3
if(a==1):
    if(b==3):
        if(a<b):
            print(0)
        print(1)
    else:
        print(2)
else:
    print(3)            # 0 1
```

## 연산자를 활용한 조건문

관계 연산자, 논리 연산자 등 각종 연산자를 활용해 복잡한 조건의 프로그램 제어 가능

1. 여러 줄의 복잡한 조건문을 한 줄로 표현 가능
    > True일 경우 if 조건식, False일 경우 else 조건식

```py
a = 1
if(a == 1):
    msg = 'a is 1'
else:
    msg = 'a is not 1'
print(msg)              # a is 1

msg2 = "a is 1" if (a == 1) else "a is not 1"
print(msg2)             #
```