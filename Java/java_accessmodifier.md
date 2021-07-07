# Java 접근제어자

접근 제어자는 클래스의 멤버(변수, 메서드)들의 **접근 권한을 지정**한다.     

```java
class A {
    public String y(){
        return "public void y()";
    }
    private String z(){
        return "public void z()";
    }
    public String x(){
        return z();
    }
}

public class AccessDemo1{
    public static void main(String[] args){
        A a = new A();
        System.out.println(a.y());
        System.out.println(a.z());      // 메서드 z에 접근 불가
        System.out.println(a.x());        
    }
}
```

### public

```java
public class Everywhere {
    public String var = "누구든지 허용"; // public 필드
    public String getVar() {             // public 메소드
        return this.var;
    }
}
```

**public** 접근 제어자는 프로그램 어디서나 직접 접근할 수 있다.     
또한 private 멤버와 프로그램에 접근할 수 있게 하는 역할을 수행한다.

### private

```java
public class SameClass {
    private String var = "같은 클래스만 허용"; // private 필드
    private String getVar() {                  // private 메소드
        return this.var;
    }
}
```

**private** 접근 제어자를 사용하여 선언된 클래스 멤버는 외부에 공개되지 않으며 외부에서 접근할 수 없다.     
해당 객체의 public 메서드를 통해서만 접근할 수 있으며 클래스 내부의 세부적인 동작을 구현하는 데 사용한다.