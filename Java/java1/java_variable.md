# Variable

```java
public class Variable
{

	public static void main(String[] args)
	{
		int a = 1; // Number => integer
		System.out.println(a);

		double b = 1.1; // Real number => double
		System.out.println(b);

		String c = "Hello World";
		System.out.println(c);
	}

}
```

- 자바에서는 **변수**를 지정할 때 데이터 타입을 지정해야 한다
- **int**는 정수, **double**은 실수, **String**은 문자열값만 들어갈 수 있다

```java

public class Letter
{

	public static void main(String[] args)
	{
		String name = "sian";
		System.out.println("Hello, " + name + " ... bye");

		double VAT = 10.0;
		System.out.println(VAT);

        String string = "string"; // Nope
	}

}
```

- **변수**는 값의 이름을 지어주는 것으로 명확하게 지어야 한다
- **숫자**로 시작하거나 `_`와 `$` 이외의 특수문자, 자바의 키워드는 변수명으로 사용할 수 없다

```java
public class Casting {
 
    public static void main(String[] args) 
	{
        double a = 1.1;
        double b = 1;
        double b2 = (double) 1;
         
        System.out.println(b);
         
        // int c = 1.1;
        double d = 1.1;
        int e = (int) 1.1;
        System.out.println(e);
         
        // 1 to String 
        String f = Integer.toString(1);
        System.out.println(f.getClass());
    }
}
```

- **Casting(형변환)**은 변수 또는 리터럴의 타입을 다른 타입으로 변환하는 것이다
- 정보의 누락, 손실이 발생하는 경우 수동으로 캐스팅해야 한다
- 수동 캐스팅은 **(타입이름)피연산자** 식으로 쓴다
- `double b = 1;`에서 에러가 나지 않은 것은 **손실**이 없기 때문이다
