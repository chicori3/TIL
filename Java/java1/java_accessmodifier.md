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
        System.out.println(a.z()); // 메서드 z에 접근 불가
        System.out.println(a.x());        
    }
}
```

### public

```java
public class Everywhere {
    public String var = "누구든지 허용"; // public 필드
    public String getVar() { // public 메소드
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
    private String getVar() { // private 메소드
        return this.var;
    }
}
```

**private** 접근 제어자를 사용하여 선언된 클래스 멤버는 외부에 공개되지 않으며 외부에서 접근할 수 없다.     
해당 객체의 public 메서드를 통해서만 접근할 수 있으며 클래스 내부의 세부적인 동작을 구현하는 데 사용한다.

### default

```java
// 같은 패키지만 접근 허용
package test;

public class SamePackage {
    String sameVar = "같은 패키지는 허용"; // default 필드
}
// 같은 클래스도 접근 허용
package test;

public class SameClass {
    String var = "다른 패키지는 접근 불가"; // default 필드
    public static void main(String[] args) {
        SamePackage sp = new SamePackage();
        System.out.println(sp.sameVar); // 같은 패키지는 허용
    }
}
```

**default** 접근 제어자는 클래스, 클래스 멤버 접근 제어의 기본값으로 접근 제어자가 지정되지 않으면 자동적으로 설정된다.     
default 접근 제어를 가지는 멤버는 같은 클래스의 멤버와 같은 패키지에 속하는 멤버에서만 접근할 수 있다.

### protected

```java
// 같은 패키지는 접근 허용
package test;

public class SameClass {
    protected String sameVar = "다른 패키지에 속하는 자식 클래스까지 허용"; // protected 필드
}
// 다른 패키지에 속하는 자식 클래스도 접근 허용
package test.other;

import test.SameClass; // test 패키지의 SameClass 클래스를 불러들여 포함시킴.

public class ChildClass extends SameClass {
    public static void main(String[] args) {
        SameClass = new SameClass();
        System.out.println(sp.sameVar); // 다른 패키지에 속하는 자식 클래스까지 허용
    }
}
```

**protected** 멤버는 부모 클래스에 대해서는 public 멤버, 외부에서는 private 멤버처럼 취급된다.      
1. 이 멤버를 선언한 클래스의 멤버
2. 이 멤버를 선언한 클래스가 속한 패키지의 멤버
3. 이 멤버를 선언한 클래스를 상속받은 자식 클래스의 멤버

## 접근 제어자의 접근 범위

|접근 제어자|같은 클래스|같은 패키지|자식 클래스|그 외의 영역
|:-:|:-:|:-:|:-:|:-:
|public|O|O|O|O
|protected|O|O|O|X
|default|O|O|X|X
|private|O|X|X|X
