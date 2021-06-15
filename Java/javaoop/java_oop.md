# 자바 객체 지향 프로그래밍

## 객체 지향과 절차 지향

먼저 **객체 지향 프로그래밍(OOP)** 과 **절차 지향 프로그래밍(PP)** 은 반대 개념이 아니다.     
PP는 **데이터를 중심으로 함수**를 만들어 사용하는 편이고, OOP는 **데이터와 기능(함수)를 묶어 하나의 객체**로 만들어 사용한다.       

Java에서 PP는 **메서드를 이용해** 작은 부품을 만들고 더 큰 프로그램을 만드는 것이다.          
반면 OOP는 서로 연관된 메서드와 변수들을 결합한 **클래스를 중심으로 프로그래밍하는 것**으로 볼 수 있다.

![클래스](./images/java_oop_01.png)
>출처 : 생활코딩(https://opentutorials.org/)

#### 절차 지향 프로그래밍의 특징        
    1. 객체나 클래스를 만들 필요 없이 프로그램을 코딩할 수 있다     
    2. 필요한 기능을 함수로 만들어 두기 때문에 같은 코드를 복사하지 않고 호출하여 사용할 수 있다        
    3. 프로그램의 흐름을 쉽게 추적할 수 있다        
    4. 각 코드가 유기성이 높기 때문에 수정하기가 힘들다     
    5. 코드를 재사용할 수 없어 개발 비용과 시간이 늘어날 수 있다        
    6. 디버그가 어렵다      

#### 객체 지향 프로그래밍의 특징        
    1. 모듈화, 캡슐화로 인해 유지보수에 용이하다        
    2. 객체 지향적이기 때문에 현실 세계와 유사성에 의해 코드를 이해하기 쉽게 만든다     
    3. 다른 프로그램에서 재사용이 가능하다      
    4. 속도가 상대적으로 느리고 많은 양의 메모리를 사용하는 경향이 있다     
    5. 설계 과정에 시간이 많이 투자된다     


## 클래스, 메서드와 변수

```java
// MyOOP.java
public class MyOOP {
    public static void main(String[] args) {
        Print.delimiter = "----";
        Print.A();        
        Print.B();

        Print.delimiter = "****";
        Print.A();
        Print.B();
    }
}

// Print.java
class Print { // 클래스
    public static String delimiter = ""; // 전역 변수

    public static void A() { // 메서드
        System.out.println(delimiter);
        System.out.println("A");
        System.out.println("A");
    }

    public static void B() {
        System.out.println(delimiter);
        System.out.println("B");
        System.out.println("B");
    }
}

```

연관성이 있는 반복되는 코드를 그룹핑하여 **메서드**로 만든다.    
반복되는 값은 **변수**로 설정하며 메서드 내부에서 정의된 변수는 메서드 밖에서 사용할 수 가 없다. 때문에 **전역 변수**로 선언하면 관리가 편하다.   
**클래스**는 이러한 메서드와 변수를 그룹핑한 것으로 훨씬 간결하고 좋은 코드를 짤 수 있게 된다. 또한 외부에서도 사용할 수 있어서 따로 만들어 호출하여 사용할 수 있다.

## 인스턴스

![java_oop_02](./images/java_oop_02.png)
>출처 : 생활코딩(https://opentutorials.org/)

냉장고를 클래스라고 생각해보자. 똑같은 냉장고를 여러 개를 만들어 안에 다양한 재료로 채울 수 있다. **인스턴스**가 바로 복제된 냉장고다.      
똑같은 냉장고를 만들 땐 `new`를 붙여준다.

```java
// MyOOP.java
public class MyOOP {
    public static void main(String[] args) {
        Print p1 = new Print();
        p1.delimiter = "----";
        p1.A();        
        p1.B();

        Print p2 = new Print();
        p2.delimiter = "****";
        p2.A();
        p2.B();

        // Print.delimiter = "----";
        p1.A();
        // Print.delimiter = "****";
        p2.A();
        p1.B();
        p2.B();
    }
}

// Print.java
class Print { // 클래스
    public static String delimiter = ""; // 전역 변수

    public void A() { // 메서드
        System.out.println(delimiter);
        System.out.println("A");
        System.out.println("A");
    }

    public void B() {
        System.out.println(delimiter);
        System.out.println("B");
        System.out.println("B");
    }
}

```

`delimiter`를 매번 바꾸는 것은 번거로운 일이며 효율적이지 않다. 인스턴스를 사용하면 더 쉽게 작업이 가능해진다.      
인스턴스를 사용하기 전에 `static`은 항상 값이 변하지 않는 경우에 사용하는 데 지금은 `delimeter` 변수의 값을 변경할테니 지워준다.     
`Print p1 = new Print();`는 Print 데이터 타입의 Print 클래스를 p1 객체에 담는다라고 할 수 있다.         
p1과 p2의 delimeter 변수값을 설정함으로써 같은 클래스를 돌려막지 않아도 된다.

## static

```java
class Foo {
    public static String classVar = "I class var"; // static 변수 (클래스 필드)
    public String instanceVar = "I instance var"; // non-static 변수 (인스턴스 필드)

    public static void classMethod() { // 클래스의 static 메서드가 클래스의 변수에 접근이 가능할까?
        System.out.println(classVar); // static 메서드는 static 변수에 접근 가능
//      System.out.println(instanceVar); // 인스턴스 변수에는 접근 불가능
    }

    public void instanceMethod() { // 인스턴스 메서드는 클래스의 변수에 접근이 가능할까?
        System.out.println(classVar); // 인스턴스 메서드는 static 변수에 접근 가능
        System.out.println(instanceVar); // 인스턴스 변수에도 접근 가능
    }
}

public class StaticApp {

    public static void main(String[] args) {
        System.out.println(Foo.classVar); // Foo 클래스의 static 변수에 접근 가능
//      System.out.println(Foo.instanceVar); // 인스턴스 변수에 접근 불가능
        Foo.classMethod(); // static 메서드에 접근 가능
//      Foo.instanceMethod(); // 인스턴스 메서드에 접근 불가능

        // Foo f1, f2 인스턴스 생성
        Foo f1 = new Foo(); 
        Foo f2 = new Foo();
      
        System.out.println(f1.classVar); // I class var
        System.out.println(f1.instanceVar); // I instance var
      
        f1.classVar = "changed by f1";
        System.out.println(Foo.classVar); // changed by f1
        System.out.println(f2.classVar); // changed by f1
      
        f1.instanceVar = "changed by f1";
        System.out.println(f1.instanceVar); // changed by f1
        System.out.println(f2.instanceVar); // I instance var
    }

}
```

![java_oop_03](./images/java_oop_03.png)

**static** 키워드로 변수나 메서드 앞에 붙여 static 변수와 메서드를 만들 수 있다. 클래스 멤버라고도 하는 데, 모든 객체가 메모리를 공유하는 특징이 있다.     

```java
static int num = 0; // static 변수 선언
public static void static_method(){} // static 리턴 타입 메소드 {}
```

static으로 선언된 변수와 메서드는 같은 메모리를 가리키므로 `Foo.classVar`와 인스턴스 `f1.classVar`, `f2.classVar`는 같은 메모리를 사용한다.    
`f1.classVar = "changed by f1";` 로 static 변수값을 변경하면 Foo와 f1, f2의 classVar가 다 똑같은 변수값을 가리키게 된다.        
하지만 인스턴스는 각 다른 객체이므로 `f1.instanceVar = "changed by f1";` 를 작성하면 f1의 instanceVar 값만 바뀌게 된다.