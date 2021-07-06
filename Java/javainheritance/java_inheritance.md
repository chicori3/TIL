# Java 상속

```java
class Cal {
    public int sum(int v1, int v2) {
        return v1 + v2;
    }
}

class Cal2 extends Cal { // 상속
    public int minus(int v1, int v2) {
        return v1 - v2;
    }
}


public class InheritanceApp {

    public static void main(String[] args) {
        Cal2 c = new Cal2();
        System.out.println(c.sum(2, 1));
        System.out.println(c.minus(2, 1));

    }

}
```

클래스 **상속**을 위해서는 `extends` 키워드를 사용한다.
```
자식클래스 extends 부모클래스
```
`Cal2` 클래스는 `Cal` 클래스를 상속받고 `minus()` 메서드를 추가한 상태이다. `Cal2` 클래스에는 `sum()` 메서드가 없지만 부모로부터 상속을 받았기에 이상없이 호출이 된다. 상속받은 자식 클래스는 부모 클래스에 이것 저것 기능을 더 추가할 수 있다.

## Overriding vs Overloading

```java
class Cal {
    public int sum(int v1, int v2) {
        return v1 + v2;
    }
    // Overloading
     public int sum(int v1, int v2, int v3) {
        return v1 + v2 + v3;
    }
}

class Cal2 extends Cal { // 상속
    public int minus(int v1, int v2) {
        return v1 - v2;
    }
    // Overriding
     public int sum(int v1, int v2) {
        System.out.println("Cal2!!")
        return v1 + v2;
    }
}


public class InheritanceApp {

    public static void main(String[] args) {
        Cal2 c = new Cal2();
        System.out.println(c.sum(2, 1));

        System.out.println(c.sum(2,1,1));

        System.out.println(c.minus(2, 1));

    }

}
```

**Overrding**은 부모 클래스의 메서드를 자식 클래스에서 재정의하는 것이다.

1. 메서드의 동작만을 재정의하는 것으로 메서드의 선언부는 기존과 같아야 한다
2. 메서드의 반환 타입은 변환할 수 있는 타입이라면 변경 가능
3. 부모 클래스의 메서드보다 접근 제어자를 더 좁은 범위로 변경할 수 없다
4. 부모 클래스의 메서드보다 더 큰 범위의 예외를 선언할 수 없다

**Overloading**은 새로운 메서드를 정의하는 것으로 상속과는 관계 없다.
