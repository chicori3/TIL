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

## this & super

```java
class Cal {
    public int sum(int v1, int v2) {
        return v1 + v2;
    }
    // Overloading
     public int sum(int v1, int v2, int v3) {
        return this.sum(v1, v2) + v3;
    }
}

class Cal2 extends Cal { // 상속
    public int minus(int v1, int v2) {
        return v1 - v2;
    }
    // Overriding
     public int sum(int v1, int v2) {
        System.out.println("Cal2!!")
        return super.sum(v1 + v2);
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

- this : 현재 클래스의 인스턴스

- this() : 현재 클래스에 정의된 생성자를 호출할 때 사용
- super : 부모 클래스의 멤버
- super() : 부모 클래스의 생성자를 호출할 때 사용
    > 기본적으로 생략해도 super가 정의되어 있음

## 상속과 생성자

```java
class Cal{
    int v1,v2;
    Cal(int v1, int v2){                // 생성자
        System.out.println("Cal init!!");
        this.v1 = v1; this.v2 = v2;
    }
    public int sum(){
        return this.v1+v2;
    }
}
class Cal3 extends Cal{
    Cal3(int v1, int v2) {
        super(v1, v2);                  // 부모 클래스의 생성자
        System.out.println("Cal3 init!!");
    }
    public int minus(){
        return this.v1-v2;
    }
}
public class InheritanceApp {
    public static void main(String[] args) {
        Cal c = new Cal(2,1);
        Cal3 c3 = new Cal3(2, 1);
        System.out.println(c3.sum());   // 3
        System.out.println(c3.minus()); // 1
    }
}
```

부모 클래스에 생성자가 있으면 자식 클래스는 반드시 생성자를 상속하여야 한다.    
`super(v1, v2);` 는 부모 클래스의 생성자 함수를 실행시킨다.     
그 결과 자식 클래스인 `Cal3`을 호출하면 우선 부모 클래스 `Cal` 생성자가 먼저 호출되고 `Cal3`이 호출되는 것을 확인할 수 있다.    
`minus()` 메서드는 자신이 가지고 있으니까 실행이 되고, `sum()`은 자신에게 정의되지 않았기 때문에 부모 클래스의 메서드를 실행시킨다.

