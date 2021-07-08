# Java 데이터 타입과 메모리 영역

## 1. Java 데이터 타입의 분류

프로그램은 자료구조(데이터)와 알고리즘의 결합으로 이루어진다.	
Java의 데이터 타입은 **기본 타입**과 **참조 타입**으로 분류된다.

### 1. 기본 타입

```java
// 기본 데이터 타입
byte b = 1;
char c = 'a'					// 한 글자
int i = 1000;					// 정수 리터럴

float f = 3.14f;
double	d = 3.141592;			// 실수 리터럴

// 형변환
int i2 = 'A';			
System.out.println(i2); 		// 97 (아스키코드)
System.out.println((char)i2);	// 'A'

// Overflow
int i3 = (int)1000000000000l;
System.out.println(i3);			// -727379968 
```

1. 정수
	- byte : 1byte 8bit
	- char : 2byte 16bit
	- short : 2byte 16bit
	- **int** : 4byte 32bit
		> 정수 기본값
	- long : 8byte 64bit

2. 실수
	- float : 4byte 16bit
	- **double** : 8byte 64bit
		> 실수 기본값

3. 논리
	- boolean : 1byte 8bit
		> true, false

**기본 데이터 타입이란 정수, 실수, 문자, 논리 리터럴을 직접 저장하는 타입을 말한다.**
메모리는 최소 기억 단위인 **bit**, 8개 bit를 묶은 **byte**가 있다.	
**오버플로우 현상**은 데이터 타입의 값의 범위를 초과할 때 발생하는 현상으로 엉뚱한 값이 변수에 들어가게 된다.

### 2. 참조 타입

