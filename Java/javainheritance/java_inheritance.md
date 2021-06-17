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