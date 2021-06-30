# 파이썬 클래스의 활용

## 연산자 오버로딩

- 메서드의 중복 정의

- 같은 이름의 메서드를 사용하는 것

1. 파이썬에서의 오버로딩

파이썬에서 같은 이름의 메서드를 사용하면 덮어쓰기 됨

```py
class A:
    def func(self,a):
        return 'hello'
    def func(self):
        return 'world'

a = A()
print(a.func())         # world
print(a.func(1))        # TypeError
```

2. 연산자 오버로딩

- 기존 약속되어 있는(__) `add()` 메서드를 재정의해서 해당 클래스에서 객체 간 덧셈 연산을 가능하게 함
    > 특수한 메서드

```py
a = 1
b = 2
print(a+b)  # 3

class A:
    def __init__(self,i):
        self.i = i

    # add 재정의
    def __add__(self,other):
        return self.i + other

n = A(40)
print(n+1)  # 41
```

- 인스턴스의 사칙연산
    
```py
class MyInt:
    def __init__(self, i):
        self.i = i
    def __str__(self):
        return str(self.i)
    def __add__(self, other):
        return self.i + other
    def __sub__(self, other):
        return self.i - other

i = MyInt(10)
print(str(i))   # 10
i = i + 10
print(i)        # 20
i += 15
print(i)        # 35
i *= 10
print(i)        # TypeError
```

> 연산자 오버로딩을 하지 않으면 인스턴스 간 연산 불가

### 연산자 오버로딩의 종류와 활용

1. 수치 연산자 오버로딩

- 해당 메서드들을 클래스에 오버로딩하면 연산자를 활용해 인스턴스의 연산이 가능
    > 나누기의 경우 div에서 truediv로 변경

|메서드|연산자|예시
|:-:|:-:|:-:
|`__add__(self,B)`| + (이항) | A + B, A += B
|`__sub__(self,B)`| - (이항) | A - B, A -= B
|`__mul__(self,B)`| * | A * B, A*= B
|`__truediv__(self,B)`| / | A / B, A /= B

- 연산자 왼쪽에 피연산자, 연산자 오른쪽에 객체가 오는 경우
    > 메서드 앞에 r을 붙여야 함

2. 비교 연산자 오버로딩

|메서드|연산자
|:-:|:-:
|`__lt__(self,other)`|self < other
|`__le__(self,other)`|self <= other
|`__eq__(self,other)`|self == other
|`__ne__(self,other)`|self != other
|`__gt__(self,other)`|self > other
|`__ge__(self,other)`|self >= other

3. 시퀀스 / 매핑 자료형의 연산자 오버로딩

- 클래스에 다음 연산자들을 활용해 자신만의 시퀀스 자료형을 만들 수 있음

- 내장 자료형과 개발자가 정의한 자료형에 대해 일관된 연산 적용 가능

|메서드|연산자
|:-:|:-:
|`__len__(self)`|len()
|`__contians__(self,item)`|item in self
|`__getitem__(self,key)`|self[key]
|`__setitem__(self,key,value)`|self[key] = value
|`__delitem__(self,key)`|del self(k)

4. 올바른 연산자 오버로딩

`isinstance` : 해당 객체가 어떤 클래스로부터 만들어졌는지 확인

```py
class A:
    def __init__(self, i):
        self.i = i
    def __add__(self, other):
        return self.i + other

i = A(10)
i = i+1
print(i)                # 11
print(type(i))          # <class 'int'>
print(isinstance(i,A))  # False

class B:
    def __init__(self, i):
        self.i = i
    def __add__(self, other):
        return B(self.i + other)

i = B(10)
i = i+1
print(i)                # <__main__.B object at 0x7f4797ce9280>1
print(type(i))          # <class '__main__.B'>
print(isinstance(i,B))  # True
```

## 상속

클래스의 속성, 메서드를 자식이 물려받는 것

- 상속받은 자식 클래스는 부모 클래스의 속성과 메서드를 사용할 수 있음

- 자식 클래스의 이름 공간에 부모 클래스의 이름 공간이 포함됨

### 상속의 이유

1. 코드를 재사용 할 수 있음

2. 상속받은 자식 클래스는 부모 클래스의 모든 기능 사용 가능
3. 자식 클래스는 필요한 기능만 정의하거나, 기존의 기능을 변경할 수 있음

```py
class Country:          # 부모 클래스
    name = '국가명'
    population = '인구'
    capital = '수도'

    def show(self):
        print('국가 클래스의 메소드입니다.')


class Korea(Country):   # 자식 클래스
    """Sub Class"""

    def __init__(self, name):
        self.name = name

    def show_name(self):
        print('국가 이름은 : ', self.name)
```

### 메서드 오버라이딩

자식 클래스에서 부모 클래스에 정의된 메서드를 재정의하여 대치하는 것

```py
class Korea(Country):       
    def __init__(self, name):
        self.name = name

    # show 메서드 오버라이딩
    def show(self):
        print(
            '''
            국가의 이름은 {} 입니다.
            국가의 인구는 {} 입니다.
            국가의 수도는 {} 입니다.
            '''.format(self.name,self.population,self.capital)
        )

a = Korea('한국','50000k', '서울')
a.show()

# 국가의 이름은 한국 입니다.
# 국가의 인구는 50000k 입니다.
# 국가의 수도는 서울 입니다.
```

## 다형성

다른 클래스의 같은 이름을 가진 인스턴스들이 동일한 메서드 이름으로 호출할 경우 동적으로 선택되어 수행
> 다양한 형태를 가질 수 있다

1. 다른 클래스에 속한 같은 이름의 메서드들에게 유사한 작업을 수행시킬 수 있음

2. 추상클래스를 상속하는 다른 서브클래스 내에 작성된 같은 이름의 메서드를 다른 목적으로 사용할 수 있음

### 파이썬에서의 다형성

1. 자료형의 타입이 동적으로 결정되므로 훨씬 용이함

```py
class Animal:
    def cry(self):
        return '으앙'

class Dog(Animal):
    def cry(self,a,b):
        return a * b

class Fish(Animal):
    def cry(self,a,b):
        return a + b

a = Animal()
b = Dog()
c = Fish()

print(a.cry())           # 으앙
print(b.cry('멍멍',3))    # 멍멍멍멍멍멍
print(c.cry(4,6))        # 10
```

## 상속 관계 알아내기

- `isinstance(인스턴스, 클래스)` : 해당 인스턴스가 해당 클래스에 속하면 True

- `issubclass(A 클래스, B 클래스)` : A 클래스가 B 클래스와 같거나 자식 클래스면 True