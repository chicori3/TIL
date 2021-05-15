# 자바의 구조

## Class

```java
public class ClassApp
{

    public static void main(String[] args)
    {
        System.out.println(Math.PI);
        System.out.println(Math.floor(1.6));
        System.out.println(Math.ceil(1.6));

    }

}
```

- 객체를 만들기 위한 설계도
- `Class`는 연관된 `변수`와 `메서드`로 구성되어 있다
- `소스 파일명은 public이 붙은 클래스와 이름이 동일`해야 한다
- 하나의 프로젝트에 여러 개의 클래스가 있어도 `소스 파일명과 동일한 클래스 앞에만 public`을 붙일 수 있다

## Instance

```java
import java.io.IOException;
import java.io.PrintWriter;

public class InstanceApp
{

    public static void main(String[] args) throws IOException
    {
        PrintWriter p1 = new PrintWriter("result1.txt");
        p1.write("Hello 1");
        p1.close();

        PrintWriter p2 = new PrintWriter("result2.txt");
        p2.write("Hello 2");
        p2.close();

    }

}
```

- 설계도를 바탕으로 구현된 실체
- `new`는 객체를 생성할 때 쓰는 키워드
- `PrintWriter` 클래스로부터 만들어진 `p1`은 인스턴스이다


*객체와 인스턴스*
> `p1`은 **객체**이며 `PrintWriter`로 만들어진 **인스턴스**라고 할 수 있다

## Inheritance (상속)

- 각 클래스는 상위 클래스의 메서드와 변수를 사용할 수 있는 데 이것이 `상속`이다
- `PrintWriter`가 `write()` 메서드를 가지고 있지 않다면 그보다 상위 클래스의 `write()`를 찾아서 실행하고 없다면 오류가 발생한다