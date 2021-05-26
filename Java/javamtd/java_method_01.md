# 메서드의 기본 형식

```java
public class WhyMethod {

    public static void main(String[] args) {

        // 100000000 줄의 코드
        printTwoTimesA();
        // 100000000 줄의 코드
        printTwoTimesA();
        // 100000000 줄의 코드
        printTwoTimesA();

    }

    public static void printTwoTimesA() {
        System.out.println("-");
        System.out.println("a");
        System.out.println("a");
    }

}
```

메서드를 사용하지 않고 자바로 프로그래밍은 불가능한 일이다. 메서드를 사용하면

1. 반복되는 코드의 양을 줄일 수 있다
2. 코드의 의미를 파악하기 쉽다
3. 코드 수정이 효율적이다