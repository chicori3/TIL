# 03. 자바스크립트 데이터 타입과 연산자

> 인사이드 자바스크립트를 참고하였습니다.

## 1. 자바스크립트 기본 타입

- **number, string, boolean** 을 비롯해 **null** 과 **undefined** 라는 타입이 있다. 그 자체가 하나의 값을 나타낸다는 것이다.
- 자바스크립트는 **느슨한 타입 체크 언어** 이다.
- var라는 한 가지 키워드로만 변수를 선언한다. 이렇게 선언된 변수에는 어떤 타입의 데이터라도 저장하는 것이 가능하다.  
  (현재에는 var을 사용하지 않는다. let과 const가 이를 대체한다. [var를 사용할 때 발생하는 문제들](https://www.daleseo.com/js-var-issues/))

```javascript
// 숫자 타입
var intNum = 10;
var floatNum = 0.1; // number

// 문자열 타입
var singleQuoteStr = "single quote string";
var doubleQuoteStr = "double quote string";
var singleChar = "a"; // string

// 불린 타입
var boolVar = true; // boolean

// undefined 타입
var emptyVar; // undefined

// null 타입
var nullVar = null; // object
```

### 1-1. 숫자

- 자바스크립트는 하나의 숫자형만 존재한다. 모든 숫자를 64비트 부동 소수점 형태로 저장하기 때문이다.
- 자바스크립트에서는 정수형이 따로 없고, 모든 숫자를 실수로 처리하므로 나눗셈 연산을 할 때는 주의해야 한다.
- 나눗셈 연산 결과에서 정수 부분만을 구하고 싶다면 _[Math.floor()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)_ 메서드를 사용하면 된다.

```javascript
var num = 5 / 2;

console.log(num); // 2.5
console.log(Math.floor(num)); // 2
```

### 1-2. 문자열

- 문자열은 '나 "로 생성한다.
- 자바스크립트에서는 C언어의 char 타입과 같이 문자 하나만을 별도로 나타내는 데이터 타입은 존재하지 않는다.
- 한 번 정의된 문자열은 변하지 않는다.
- 한 번 생성된 문자열은 수정이 불가능하다.

```javascript
// str 문자열 생성
var str = "test";
console.log(str[0], str[1], str[2], str[3]); // test

// 문자열의 첫 글자를 대문자로 변경?
str[0] = "T";
console.log(str); // test
```

### 1-3. 불린값

- 자바스크립트는 **true** 와 **false** 값을 나타내는 불린 타입을 가진다.

### 1-4. null과 undefined

- 두 타입은 자바스크립트에서 **값이 비어있음** 을 나타낸다.
- 기본적으로 값이 할당되지 않은 변수는 undefined 타입이며, undefined 타입의 변수는 변수 자체의 값 또한 undefined이다.
- 자바스크립트에서 **undefined는 타입이자, 값을 나타낸다**는 것에 주의하자.
- null 타입 변수의 경우는 개발자가 명시적으로 값이 비어있음을 나타내는 데 사용한다.
- null 타입 변수인지를 확인할 때 일치 연산자(===)를 사용해서 변수의 값을 직접 확인해야 한다.

```javascript
// null 타입 변수 생성
var nullVar = null;

console.log(typeof nullVar === null); // false
console.log(nullVar === null); // true
```

## 2. 자바스크립트 참조 타입(객체 타입)

자바스크립트에서 숫자, 문자열, 불린값, null, undefined 같은 기본 타입을 제외한 모든 값은 객체다. 따라서 배열, 함수, 정규표현식 등도 모두 결국 자바스크립트 객체로 표현된다.

자바스크립트에서 객체는 단순히 key:value 형태의 프로퍼티들을 저장하는 컨테이너로서, 컴퓨터 과학 분야에서 해시라는 자료구조와 상당히 유사하다. 자바스크립트에서 기본 타입은 하나의 값만을 가지는 데 비해, 참조 타입인 객체는 여러 개의 프로퍼티들을 포함할 수 있으며, 이러한 객체의 프로퍼티는 기본 타입의 값을 포함하거나, 다른 객체를 가리킬 수도 있다. 이러한 프로퍼티의 성질에 따라 객체의 프로퍼티는 함수로 포함할 수 있으며, 자바스크립트에서는 이러한 프로퍼티를 메서드라고 부른다.

### 2-1. 객체 생성

자바에서는 클래스를 정의하고, 클래스의 인스턴스를 생성하는 과정에서 객체가 만들어진다. 이에 비해 자바스크립트에서는 클래스라는 개념이 없고, 객체 리터럴이나 생성자 함수 등 별도의 생성 방식이 존재한다.

자바스크립트에서 객체를 생성하는 방법은 크게 세 가지가 있다. 하나는 기본 제공 Object() 객체 생성자 함수를 이용하는 방법, 그리고 객체 리터럴을 이용하는 방법, 다른 하나는 생성자 함수를 이용하는 방법이다.

#### 2-1-1. Obeject() 생성자 함수 이용

```javascript
// Obeject()를 이용해서 foo 빈 객체 생성
var foo = new Object();

// foo 객체 프로퍼티 생성
foo.name = "foo";
foo.age = 30;
foo.gender = "male";

console.log(typeof foo); // object
console.log(foo); // { name: 'foo', age: 30, gender: 'male' }
```

#### 2-1-2. 객체 리터럴 방식 이용

- 객체 리터럴은 {}를 이용해서 객체를 생성한다.
- {} 안에 아무것도 적지 않은 경우는 빈 객체가 생성되며, 중괄호 안에 "key:value" 형태로 표기하면 해당 프로퍼티가 추가된 객체를 생성할 수 있다.
- 프로퍼티 이름은 문자열이나 숫자가 올 수 있으며 프로퍼티 값은 자바스크립트의 값을 나타내는 어떤 표현식도 올 수 있다.  
  이 값이 함수일 경우 메서드라고 부른다.

```javascript
// 객체 리터럴 방식으로 foo 객체 생성
var foo = {
  name: "foo",
  age: 30,
  gender: "male",
};

console.log(typeof foo); // object
console.log(foo); // { name: 'foo', age: 30, gender: 'male' }
```
