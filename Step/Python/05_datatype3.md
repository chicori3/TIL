# 리스트, 튜플, 사전 자료형의 활용

## 리스트 자료형의 활용법

### 리스트의 기본 사용법

- 대괄호로 정의

- 내장함수 사용
- 리스트 안의 리스트
    > 다차원 배열로 사용 가능

### 리스트의 특징

- `insert()` : 해당 인덱스에 값 추가

- `pop()` : 해당 인덱스의 값 삭제
- `reverse()` : 값을 거꾸로 정렬
- `count()` : 해당 값의 개수
- `append()` : 해당 값을 요소로 추가
- `extend()` : 해당 리스트를 뒤에 가져다 붙임
- `sort()` : 오름차순으로 값 정렬(정렬 방식 변경 가능)
- `index()` : 리스트에 해당 값이 있으면 해당 값의 인덱스 반환
- `copy()` : 리스트 복사

### 리스트의 활용

1. 리스트 내포
    > 리스트를 만드는 반복문을 짧고 간결하게 만들어 줌

```py
l = []
for i in range(5):
    l.append(i)
print(l)            # [0, 1, 2, 3, 4]
```

2. 리스트를 큐(Queue)로 활용
    > 큐 : 먼저 넣은 데이터가 먼저 나오는 FIFO 구조로 저장하는 형식

```py
l = [1,2,3]
l.append(4)
print(l)            # [1,2,3,4]

l.pop(0)
print(l)            # [2,3,4]
```

3. 리스트를 스택으로 활용
    > 스택 : 나중에 넣은 데이터가 먼저 나오는 LIFO 구조로 저장하는 형식

```py
l = [1,2,3]
l.append(4)
print(l)            # [1,2,3,4]

l.pop()
print(l)            # [1,2,3]
```

## 튜플 자료형의 활용법

### 튜플의 기본 사용법

- 소괄호로 정의

- 내장함수 사용
- 원소가 하나인 튜플 정의
    > 콤마 사용

```py
t = (1)
print(type(t))      # <class 'int'>

t = (1,)
tt = 1,
print(type(t),type(tt))      # <class 'tuple'>
```

### 튜플의 특징

**값을 변경할 수 없음**

- `count()` : 해당 값의 개수
- `index()` : 해당 값의 순서, 값이 여러 개일땐 첫 번째

### 튜플의 활용

1. 값의 할당 및 리턴

```py
t = 1,2,3
x,y,z = 1,2,3
print(t)        # (1,2,3)
print(x)        # 1
print(y)        # 2
print(z)        # 3

def test():
    return (1,2)

a,b = test()
print(a)        # 1
print(b)        # 2
```

## 사전 자료형의 활용법

- 중괄호로 정의

- 내장함수 사용
- 사전에서 키는 고유한 값이므로 중복되는 키에 값을 입력하면 기존 값이 사라짐

```py
d[1] = 1
print(d)        # {1: 1}

d[1] = 2
print(d)        # {1: 2}
```

### 사전의 특징

- `update()` : 두 사전의 병합
    > a.update(b) : a사전에 b사전을 새롭게 업데이트, a값만 변경됨

- `pop()` : 해당 키의 항목 삭제
- `clear()` : 전체 삭제
- `copy()` : 사전의 복사
    > 새로운 객체를 만들어서 복사

### 사전의 활용

1. 반복문에서의 사전

```py
d = {'a':1, 'b':2, 'c':3}
for i in d:
    print(i)    # a b c

for i in d.values():
    print(i)    # 1 2 3

for i in d.items():
    print(i)    #('a', 1)('b', 2)('c', 3)
```

2. 사전에서 값의 유무 알아보기

```py
d = {'a':1, 'b':2, 'c':3}

print('a' in d)         # True
print('d' in d)         # False
print(2 in d.values())  # True
print(5 in d.values())  # False
```