# Java 연산자

## 산술 연산자

```java
int a = 5;
int b = 3;

// + 더하기
System.out.println(a+b); // 5

// - 빼기
System.out.println(a-b); // 2

// * 곱하기
System.out.println(a*b); // 15

// / 나누기
System.out.println(a/b); // 1

// % 나머지
System.out.println(a%b); // 2
```

사칙연산을 다루는 연산자로 두 개의 피연산자를 가지는 이항 연산자

## 대입 연산자

```java
int num = 7;
num += 1; // num = num + 1
num *= 3; // num = num * 3
```

변수에 갑을 대입할 때 사용하는 이항 연산자로 오른쪽에서 왼쪽으로 결합한다

## 증감 연산자

```java
int i2 = 5;
int j2 = 4;
int result = i2 + ++j2;

System.out.println(result +""+ j2); // 10 5 

result2 = i2 + j2++;
System.out.println(result2 +""+ j2); // 10 6 
```

증감 연산자는 피연산자를 1씩 증가 혹은 감소시킬 때 사용한다
**전치**와 **후치**로 나뉘며 전치의 경우 먼저 수행된 후에 연산을 하고 후치는 연산이 된 후에 수행한다

## 비교 연산자

```java
System.out.println(1 == 1); // true
System.out.println(1 != 1); // false
System.out.println(1 > 1); // false
System.out.println(1 <= 1); // true
```

비교 연산자는 피연산자 사이의 상대적인 크기를 판단한다
연산자와 피연산자를 비교해서 조건이 맞으면 **true** 아니면 **false**를 반환한다

## 논리 연산자

```java
char ch1 = 'b', ch2 = 'B';
boolean result1, result2;

result1 = (ch1 > 'a') && (ch1 < 'z') ;
result2 = (ch2 < 'A') || (ch2 < 'Z') ;

System.out.println(result1);	// true
System.out.println(result2);	// true
System.out.println(!result2);	// false
```

논리 연산자는 주어진 논리식을 판단하여 참과 거짓을 결정한다
**&&**은 and, **||**는 or, **!**는 NOT을 표현한다

## 비트 연산자

```java
int e = 3;
int f = 5;

System.out.println(e | f);	// 7
System.out.println(e & f);	// 1
```

비트 연산자는 논리 연산자와 비슷하지만 **비트 단위**로 논리 연산을 할 때 사용한다
또한 비트 단위로 왼쪽이나 오른쪽으로 전체 비트를 이동하거나, 1의 보수를 만들 때도 사용한다

## 기타 연산자

```java
// 삼항 연산자
int num1 = 5, num2 = 3;

int result = (num1 - num2 > 0) ? true : false;
System.out.println(result); // true

// instanceof 연산자
class A {}

class B extends A {}

public static void main(String[] args) {
    A a = new A();
    B b = new B();

    System.out.println(a instanceof A); // true
    System.out.println(b instanceof A); // true
    System.out.println(a instanceof B); // false
    System.out.println(b instanceof B); // true
}
```

삼항 연산자는 ? 앞의 조건식에 따라 참이면 반환값1을 반환하고 거짓이면 반환값2를 반환한다

instanceof 연산자는 참조 변수가 참조하고 있는 인스턴스의 실제 타입을 반환한다
해당 객체가 어떤 클래스나 인터페이스로부터 생성되었는지를 판별해주는 역할을 한다