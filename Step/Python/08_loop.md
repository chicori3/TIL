# 파이썬의 반복문

## for 반복문

파이썬의 제어문 중 하나로 프로그램의 실행을 반복할 수 있음

- 조건문과 마찬가지로 들여쓰기와 콜론 주의

- 반복 가능한 객체를 순회하며 반복문 안의 코드를 한 번씩 실행

`for 아이템 in 반복 가능한 객체: 실행코드`

    1. 반복 객체에서 순서대로 하나씩 값을 가져옴

    2. 아이템에 가져온 값을 담음
    3. 실행 코드 수행
    4. 반복 객체가 끝날 때까지 순차적으로 반복

1. 리스트 튜플 등 집합 자료형을 사용하여 요소를 하나씩 가져와 반복 가능

2. 반복 가능 객체인 문자열, 사전, 집합 자료형으로도 반복문 사용 가능

```py
for a in {1,2,3}:
    print(a)

for b in [1,2,3]:
    print(b)

for c in 'Hello':
    print(c)
```

## 반복 객체 및 range 함수

### 반복 객체 함수

Iterable 객체란 뜻으로 객체의 멤버를 하나씩 반환할 수 있음

- 대표적으로 시퀀스 데이터 타입인 리스트, 튜플, 스트링 등이 있음

- collections.Iterable에 속한 인스턴스인지 아닌지로 반복 가능한 객체를 판별할 수 있음

```py
import collections
obj1 = [1,2,3,4]
isinstance(obj, collections.Iterable)   # True

obj2 = ['Hello']
isinstance(obj, collections.Iterable)   # True
```

### range 함수

반복 가능한 객체를 반환해주는 함수

- range(시작(이상), 끝(미만), 스텝)으로 정의
    > 시작과 스텝은 생략 가능

- 반복문에 많이 활용
- 순차적으로 값을 반환하기 때문에 리스트 등의 다른 자료형과 함께 사용할 수 있음

```py
print(range(10))                        # range(0,10)

l = list(range(10))
print(l)                                # [0,1,2,3,4,5,6,7,8,9]

import collections
obj = range(10)
isinstance(obj, collections.Iterable)   # True
```

## 반복문 활용

1. 반복 객체의 값을 바로 가져와서 사용하거나, `range()`, `len()` 함수를 활용해 인덱스로 접근 또한 가능

```py
l1 = ['a',9,[1,2],('a','b')]
for i in l1:
    print(i)        # a 9 [1, 2] ('a', 'b')


l2 = ['a',9,[1,2],('a','b')]
for i in range(len(l2)):
    print(l[i])     # a 9 [1, 2] ('a', 'b')
```

2. 반복문을 여러 개 사용할 경우, 들여쓰기 주의
3. 요소 값을 아이템 변수로 할당하여 응용 가능

```py
l1 = [[1,2],[3,4],[5,6]]
for i in l1:
    print(i)        # [1,2] [3,4] [5,6]

l2 = [[1,2],[3,4],[5,6]]
for i in l2:
    print(i+j)      # 3 7 11
```

4. 조건문과 함께 사용해 복잡한 프로그램 작성 가능
5. `continue`를 활용해 한 차례 반복을 건너뛸 수 있음

```py
s = 'Hello'
cnt = 0
for i in s:
    if(i == 'e'):
        print('i is e')
        continue    # continue가 없다면 5가 출력됨
    cnt +=1
print(cnt)          # i is e
                    # 4
```

## while 반복문

파이썬의 제어문 중 하나로 프로그램의 실행을 반복할 수 있음

- 무한루프에 빠지지 않도록 조건 설정 주의

```py
while(True):
    print(1)        # 1 무한 출력
```

### while 반복문의 활용

1. 조건문과 `break` 보조 제어문을 활용해 특별한 조건에서 반복문을 빠져나올 수 있음

```py
num = 10
while(num > 0):
    if(num == 6):
        print("--end--")
        break
    print(num)
    num -= 1        # 10 9 8 7 --end--
```

2. 조건문과 `continue` 보조 제어문을 활용해 특별한 조건에서 해당 반복을 건너뛸 수 있음

```py
num = 5
while(num > 0):
    print(num)
    num -= 1
    if(num == 3):
        continue    # 5 4 3 2 1 
    
    
num = 5
while(num > 0):
    print(num)
    if(num == 3):
        continue
    num -= 1        # 5 4 3 3 3 3 3 3 3 ...
```

## 리스트 내포

### 리스트 내포의 정의

리스트를 만드는 반복문을 짧고 간결하게 만들어 줌

`[식 for 변수 in 반복 가능한 객체]`

```py
l = []
for i in range(5):
    l.append(i)
print(l)                        # [0, 1, 2, 3, 4]

print([i for i in range(5)])    # [0, 1, 2, 3, 4]
```

### 리스트 내포의 활용

1. 조건문을 함께 사용할 수 있음

```py
l = []
for i in range(5):
    if(i%2 == 0):
        l.append(i)
print(l)                                    # [0, 2, 4]

print([i for i in ragne(5) if i%2 == 0])    # [0, 2, 4]
```

2. 반복문을 여러 개 사용할 수 있음

```py
l = []
for i in range(3):
    for j in range(3):
        l.append(i+j)
print(l)                # [0, 1, 2, 1, 2, 3, 2, 3, 4]

print([i+j for i in range(3) for j in range(3)])
# [0, 1, 2, 1, 2, 3, 2, 3, 4]
```