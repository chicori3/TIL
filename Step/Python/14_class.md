# 파이썬의 클래스

## 객체지향 프로그래밍

- 컴퓨터 프로그래밍의 패러다임 중 하나

- 여러 개의 독립된 **객체**의 모임으로 파악하고자 하는 것
- 프로그램을 유연하고 변경이 용이해 대규모 SW 개발에 많이 사용
- 개발과 유지보수가 간편하고 직관적인 코드 분석
- 추상화, 캡슐화, 정보은닉, 상속, 다형성, 동적 바인딩, 오버로딩 등의 특성

> **절차지향 프로그래밍**
> - 위에서 아래로 순서대로 실행
> - 프로그램이 유기적으로 연결
> - 실행 속도가 빠르지만 유지보수, 코드의 재사용이 어려움

### 프로그래밍을 할 때 주의할 점

1. 같은 코드를 반복하지 않음

2. **한번 작성한 코드는 언제든 바뀔 수 있다는 것**을 생각

## 클래스

객체를 더 효율적으로 생성하기 위해 만들어진 구문

- 소문자로 class 정의

- **인스턴스** : 클래스로부터 만들어진 객체

### 클래스와 이름공간

1. 클래스는 별도의 이름 공간이 할당

```py
class Simple_class:
    pass

c1 = Simple_class()
c2 = Simple_class()

c1.a = 10
print(c1.a)         # 10
print(c2.a)         # Attribute Error
```

2. 인스턴스 또한 별도의 이름 공간 할당
    > 동적으로 인스턴스 내부에 멤버 추가가능
    > 인스턴스마다 모두 독립적인 이름 공간

```py
a = 0
class S1:
    a = 1

print(S1.a)     # 1
x = S1()
print(x.a)      # 1

x.a = 10
print(a)        # 0 
print(x.a)      # 10
print(S1.a)     # 1
```

## 메서드

클래스가 가지고 있는 함수

- 일반적인 함수와 똑같이 정의하지만 첫 번째 매개변수로 `self` 사용 (관례적)

- `self`는 인스턴스 객체 자신의 레퍼런스를 지니고 있음
    > 각 인스턴스들은 self를 활용해 자신의 이름 공간에 접근 가능

```py
class MyClass:
    def class_set(self,v):
        self.value = v
    def class_get(self):
        return self.value
```

### 메서드의 호출

1. 인스턴스 객체를 활용한 메서드 호출
    > self 인자 활용

2. 클래스 객체를 이용한 메서드 호출

```py
class MyClass:
    def class_set(self,v):
        self.value = v
    def class_get(self):
        return self.value

c = MyClass()               # 인스턴스 생성
c.class_set('10')
print(c.class_get())        # 인스턴스 객체를 활용해 메서드 호출

c = MyClass()
MyClass.class_set(c,'10')   # 클래스 객체를 활용해 메서드 호출
print(MyClass.class_get(c))
```

### 객체 내부 메서드의 호출

1. 객체 내부의 메서드를 호출할 수 있음

2. `self`를 적지 않으면 외부에서 해당 메서드를 찾게 됨

```py
def class_set(i):
    print("외부함수 ", i)

class MyClass:
    def class_set(self,v):
        self.value = v
    def class_get(self):
        return self.value
    def class_incr(self):
        class_set(self.value + 1)       # self 없음
    def class_incr2(self):
        self.class_set(self.value + 1)  # 내부 메서드 호출

c = MyClass()               
c.class_set(1)
print(c.class_get())                    # 1

c.class_incr()                          # 외부함수 2

c.class_incr2()
print(c.class_get())                    # 2
```

### 정적 메서드

인스턴스 객체와 무관하게 클래스 이름 공간에 존재하는 메서드

- 클래스 이름을 이용해 직접 호출 가능

- 장식자 `@staticmethod` 사용

```py
class C:
    def ham(self,x,y):                  # self 사용
        print('instance method',x,y)

c = C()
c.ham(1, 2)                             # instance method 1 2

# 인스턴스 객체 없이 클래스에서 직접 호출
C.ham(1,2)                              # TypeError

class D:
    @staticmethod
    def spam(x,y):                      # self 없음
        print('static method',x,y)

# 인스턴스 객체 없이 클래스에서 직접 호출
d.spam(1, 2)                            # static method 1 2

d = D()
# 인스턴스 객체를 통해서도 호출 가능
d.spam(1, 2)                            # static method 1 2
```

## 생성자와 소멸자

### 클래스 멤버

클래스 이름 공간에 생성, 모든 인스턴스에 공유

```py
class Var:
    # 클래스 변수
    c_mem = 100
    def f(self):
        self.i_mem = 200
```

### 인스턴스 멤버

인스턴스 이름 공간에 생성, 인스턴스마다 독립

```py
class Var:
    c_mem = 100             # 클래스 변수
    def f(self):
        self.i_mem = 200

# 인스턴스 생성
v1 = Var()
v2 = Var()

v1.c_mem = 50               # 인스턴스 v1의 요소 값 변경

print(v1.c_mem)             # 50
print(v2.c_mem)             # 100
print(Var.c_mem)            # 100
```

### 생성자

객체가 생성될 때 자동으로 호출되는 함수

- `__init__`으로 정의

- 객체가 보유해야 할 변수나 자원들의 초기화를 하는 코드를 작성

```py
class MyClass:
    def __init__(self):
        self.name = "Class"
        print('Class Created. ', self.name)
c = MyClass()
# Class Created. Class
```

### 소멸자

객체가 소멸될 때 자동으로 호출되는 함수

- `__del__`로 정의

- 객체가 점유하고 있는 메모리나 기타 자원들의 해제를 하는 코드 작성

```py
class MyClass:
    def __init__(self):
        self.name = "Class"
        print('Class Created. ', self.name)
    def __del__(self):
        print('Class Deleted. ')
c = MyClass()
# Class Created. Class
# Class Deleted
```