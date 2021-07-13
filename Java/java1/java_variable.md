### 변수

**하나의 값을 저장**하는 메모리 공간

### 변수의 선언

값을 저장할 공간을 마련하기 위해 선언한다

```java
int age; // 선언
age = 27; // 초기화
String s = "dev"; // 선언과 동시에 초기화
```
지역 변수는 읽기 전에 꼭 초기화 해야 함

### 변수, 상수, 리터럴

변수 : 하나의 값을 저장하기 위한 공간, 변경 가능
상수 : **한 번만 값을 저장**하는 공간, 변경 불가능
리터럴 : 그 자체로 값을 의미하는 것

```java
int score = 100;
score = 200; // 변경 가능

final int MAX = 100; // MAX는 상수
MAX = 200; // 에러
```

### 데이터 타입

데이터 타입은 **기본 타입**과 **참조 타입**으로 분류된다.

```java
// 기본 데이터 타입
byte b = 1;
char c = 'a' // 한 글자
int i = 1000; // 정수 리터럴

float f = 3.14f;
double	d = 3.141592; // 실수 리터럴

// Overflow
int i3 = (int)1000000000000l;
System.out.println(i3); // -727379968 
```

1. 정수 리터럴
	- byte : 1byte 8bit
	- short : 2byte 16bit
	- **int** : 4byte 32bit
	- long : 8byte 64bit

2. 실수 리터럴
	- float : 4byte 16bit
	- **double** : 8byte 64bit

3. 문자 리터럴
	- char : 2byte 16bit

4. 논리 리터럴
	- boolean : 1byte 8bit

- 부호가 있는 정수의 범위 : -2ⁿ - ¹ ~ 2ⁿ - ¹
- 부호가 없는 정수의 범위 : 0 ~ 2ⁿ - ¹

**오버플로우 현상**은 데이터 타입의 값의 범위를 초과할 때 발생하는 현상으로 엉뚱한 값이 변수에 들어가게 된다.

#### 참조 타입

```java
String s = "ABC"; // s라는 주소에 "ABC" 저장
Date today = new Date(); // today라는 주소에 새로운 객체 생성
```

기본형을 제외한 나머지 타입 (System, String 등)
실제 값을 저장하는 대신 **메모리 주소를 저장** (4byte, 8byte)

#### 타입 변환

```java
int i2 = 'A';			
System.out.println(i2); // 97 묵시적 형변환
System.out.println((char)i2); // 'A' 명시적 형변환
```

타입 변환은 컴파일러가 자동으로 하는 **묵시적 형변환**과 직접 변환 시키는 **명시적 형변환**이 있다.		
- 묵시적 형변환 : 작은 메모리 타입을 큰 메모리 타입으로 컴파일러가 알아서 변환해준다.		
- 명시적 형변환 : 큰 메모리 타입을 작은 메모리 타입으로 직접 변환시키는 것으로 **데이터 소실**이 생긴다.

#### 변수와 리터럴의 타입

1. 범위가 변수 > 리터럴인 경우 OK

```java
int i = 'a'; // int > char
long l = 123; // long > int
double d = 3.14f; // double > float
```

2. 범위가 변수 < 리터럴인 경우 에러

```java
int i = 30_0000_0000; // int의 범위 밖
long l = 3.14f; // long < float
float f = 3.14d; // float < double
```

3. byte, short 변수에 int 리터럴 저장 가능
단, 변수의 타입의 범위 이내여야 함

```java
byte b = 100; byte의 범위에 속함
byte c = 128; byte 범위를 벗어나서 에러
```

### 문자와 문자열

```java
char ch = 'a'; // 문자
char ch2 = ''; // 에러 무조건 하나의 문자가 들어가야 함

String s = "ABC"; // 문자열
String s2 = ""; // 빈 문자열
```

문자열은 어느 타입이든 결합 시 **문자열**로 타입 변환한다

### 두 변수의 값 교환하기

```java
int x = 10, y = 20;
int tmp; // 빈 변수

tmp = x; // x의 값을 tmp에 저장
x = y; // x의 값을 y에 저장
y = tmp; // tmp의 값을 y에 저장
```

두 변수의 값을 교환하기 위해서는 하나의 빈 변수가 필요하다

### 타입 간의 변환

다른 타입 간의 연산은 피연산자들을 **먼저 모두 같은 타입으로 만든 후에 수행된다**   
메모리에 할당받은 바이트 크기가 **작은 타입에서 큰 타입으로의 타입 변환은 생략 가능**   
하지만 큰 타입에서 작은 타입으로의 변환은 **데이터의 손실 발생**

```java
// 1. 묵시적 형변환 (자동 타입 변환)

double num1 = 10;
int num2 = 3.14; // 데이터 손실
double num3 = 7.0f + 3.14;
int num4 = 9876543210L; // int 범위 밖
float num5 = 3.14; // type missmatch

// 2. 명시적 형변환 (강제 타입 변환)

int num = 1, num 2 = 4;
dobule result1 = (double) num1 / num2;
```