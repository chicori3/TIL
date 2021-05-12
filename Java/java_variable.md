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

- 자바에서는 각 데이터 타입마다 `변수`를 다르게 줘야 한다
- `int`는 정수, `double`은 실수, `String`은 문자열값만 들어갈 수 있다

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

- `변수`는 값의 이름을 지어주는 것으로 명확하게 지어야 한다
- `숫자`로 시작하거나 `_`와 `$` 이외의 특수문자, 자바의 키워드는 변수명으로 사용할 수 없다
