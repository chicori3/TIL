# Datatype and Operation

```java
public class Datatype
{
	public static void main(String[] args)
	{
		System.out.println(6); // Number
		System.out.println("6"); // String

		System.out.println(6 + 6); // 12
		System.out.println("6" + "6"); // 66
		System.out.println("6" + 6); // 66

		System.out.println(6 * 6); // 36
//		System.out.println("6" * "6");

		System.out.println("1111".length());
//		System.out.println(1111.length());

		System.out.println("Hello World"); // String
		System.out.println('H'); // Character
	}
}
```

- 숫자를 `"`로 감싸면 `String` 타입이 된다.
- JS와 달리 `'`로 감싸면 `Char` 타입이 된다.
- 데이터 타입에 따라 메소드를 사용한다.

```java
public class Number
{

	public static void main(String[] args)
	{
		System.out.println(6 + 2); // 8
		System.out.println(6 - 2); // 4
		System.out.println(6 * 2); // 12
		System.out.println(6 / 2); // 3

		System.out.println(Math.PI); // 3.1415...
		System.out.println(Math.floor(Math.PI)); // 3.0
		System.out.println(Math.ceil(Math.PI)); // 4.0
	}

}
```

- `Math`는 수학에서 자주 사용하는 상수들과 함수들을 미리 구현해 놓은 클래스이다.
- `Math` 클래스의 모든 메소드는 `클래스 메소드(static method)`이므로, 객체를 생성하지 않고도 바로 사용할 수 있다.

```java
public class StringApp
{

	public static void main(String[] args)
	{
		// Character & String
		System.out.println("Hello World"); // String
		System.out.println("H"); // String
		System.out.println('H'); // Character

		System.out.println("Hello " + "World"); // Hello World

		// new line
		System.out.println("Hello \nWorld"); // Hello / World

		// escape
		System.out.println("Hello \"World\""); // Hello "World"

		System.out.println("Hello World".length()); // 11
		System.out.println("Hello World".replace("Hello", "Bye")); // Bye World
	}

}
```

- `""`와 `''`의 차이가 있으니 유의할 것
- `\n`은 줄바꿈의 기능이 있다
- String 안에서 따옴표를 쓰고 싶을 땐 `\"string/"`처럼 사용한다