# Java 입력과 출력

### println

1. 자동으로 줄바꿈
2. 변수의 값을 그대로 출력
3. 값을 변환하지 않으면 다른 형식으로 출력 불가능

### printf

1. **지시자**를 통해 변수의 값을 변환 가능
2. 지시자는 출력할 값을 지정해주는 역할
3. 출력 후 줄바꿈을 하지 않음

```java
int age = 14;
System.out.printf("age : %d", age);
```

#### 지시자

|지시자|설명
|:-|:-
|%b|boolean 형식
|%d|10진 정수 형식
|%o|8진 정수 형식
|%x, %X|16진 정수 형식
|%f|부동 소수점 형식
|%e, %E|지수 표현식의 형식
|%c|문자로 출력
|%s|문자열로 출력

### Scanner

화면으로부터 데이터를 입력받는 기능을 제공하는 클래스

```java
import java.util.* // import문 추가

Scanner sc = new Scanner(System.in); // Scanner 객체 생성

int num = sc.nextInt(); // 입력받은 정수를 저장
String input = sc.nextLine(); // 입력받은 내용을 문자열로 저장
int num = Integer.parseInt(input); // 문자열을 정수로 변환
```