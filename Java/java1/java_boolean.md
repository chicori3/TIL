# Java Boolean

## Boolean

- `Boolean`에 해당하는 데이터 타입은 `true`, `false`가 있다
- `true`, `false`는 **예약어(reserved word)**라서 변수명으로 사용할 수 없다


```java
public class BooleanApp
{

	public static void main(String[] args)
	{
		System.out.println("One");
		System.out.println(1);

		// Boolean
		System.out.println(true);
		System.out.println(false);

		String foo = "Hello World";
//		String true = "Hello World"; reserved word

		System.out.println(foo.contains("World"));
		System.out.println(foo.contains("Sian"));
	}

}
```

- `contains()` 메서드는 string 변수에 해당 문자열이 포함된 여부에 따라 boolean 값을 리턴한다

## 비교연산자

```java
public class ComparisonOperator
{

	public static void main(String[] args)
	{
		System.out.println(1 > 1); // false
		System.out.println(1 == 1); // true
		System.out.println(1 >= 1); // true
	}

}
```

- `1 + 1 = 2` 에서 `+`는 산술연산자
- `"1" + "1" = "11"` 에서 `+`는 결합연산자
- 비교연산자는 값을 비교해서 그 결과값을 Boolean 타입 값으로 리턴한다