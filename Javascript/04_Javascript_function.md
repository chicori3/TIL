# 04. 함수와 프로토타입 체이닝

자바스크립트에서 가장 중요한 개념 1순위는 당연 **함수**다. 자바스크립트에서의 함수는 언뜻 보면 여느 언어와 마찬가지의 기능을 제공한다.

## 1. 함수 정의

- 함수 선언문
- 함수 표현식
- Function() 생성자 함수

## 1-1. 함수 리터럴

- 자바스크립트에서 함수는 일반 객체처럼 값으로 취급된다.
- **함수 리터럴**을 이용해 함수 생성

## 1-2. 함수 선언문 방식으로 함수 생성하기

함수 선언문 방식으로 정의된 함수의 경우는 **반드시 함수명이 정의되어 있어야 한다**.

```javascript
// add() 함수 선언문
function add(x, y) {
  return x + y;
}

console.log(add(3, 4)); // 7
```

## 1-3. 함수 표현식 방식으로 함수 생성하기

- 함수도 숫자나 문자열처럼 변수에 할당하는 것이 가능하다.
- 함수 리터럴로 하나의 함수를 만들고, 여기서 생성된 함수를 변수에 할당하여 함수를 생성하는 것을 **함수 표현식**이라고 한다.

```javascript
// add() 함수 표현식
var add = function (x, y) {
  return x + y;
};

var plus = add;

console.log(add(3, 4)); // 7
console.log(plus(5, 6)); // 11
```

- 이름이 없는 함수 형태를 **익명 함수**라고 부른다.
- 위 예제는 **익명 함수 표현식**으로 익명 함수의 호출은 함수 변수에 함수 호출 연산자인 ()를 붙여서 기술하는 것으로 가능하다.
- 함수 이름이 포함된 함수 표현식을 **기명 함수 표현식**이라고 한다.

```javascript
var add = function sum(x, y) {
  return x + y;
};

console.log(add(3, 4)); // 7
console.log(sum(3, 4)); // Uncaught RefenceError : sum is not defined
```

sum() 함수를 정의하고, add 함수 변수에 할당했다. sum() 함수 호출의 경우 에러가 발생했는 데, 이것은 **함수 표현식에서 사용된 함수 이름이 외부 코드에서 접근 불가능하기 때문이다.** 실제로 함수 표현식에 사용된 함수 이름은 정의된 함수 내부에서 해당 함수를 재귀적으로 호출하거나, 디버거 등에서 함수를 구분할 때 사용된다.

```javascript
var factorialVar = function factorial(n) {
  if (n <= 1) {
    return 1;
  }
  return n * factorial(n - 1);
};

console.log(factorialVar(3)); // 6
console.log(factorial(3)); // Uncaught RefenceError : factorial is not defined
```

- 함수 외부에서는 함수 변수 factorialVar로 함수를 호출했으며, 함수 내부에서 이뤄지는 재귀 호출은 factorial()로 처리된다.
- factorial()로 함수 외부에서 해당 함수를 호출하면 에러가 발생한다.

## 1-4. Function() 생성자 함수를 통한 함수 생성하기

- 자바스크립트의 함수도 **Function()**이라는 기본 내장 생성자 함수로부터 생성된 **객체**이다.
- 함수 선언문, 함수 표현식 방식도 결국엔 내부적으로는 Function() 생성자 함수로 함수가 생성된다고 볼 수 있다.
- 일반적으로 사용되지 않으니 알아만 두자.

```javascript
// Function() 생성자 함수 이용
var add = new Function("x", "y", "return x+y");
console.log(add(3, 4)); // 7
```

## 1-5. 함수 호이스팅

```javascript
// 함수 선언문 방식
add(2, 3); // 5

function add(x, y) {
  return x + y;
}

add(3, 4); // 7
```

- 위 예제에서 add() 함수가 정의되지 않았음에도 함수를 호출하는 것이 가능한 데, **함수 선언문 형태로 정의한 함수의 유효 범위는 코드의 맨 처음부터 시작한다**는 것을 확인할 수 있다.
- **[함수 호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)**은 자바스크립트의 **변수 생성**과 **초기화**의 작업이 분리되어 진행되기 때문에 발생한다.

```javascript
// 함수 표현식 방식
add(2, 3); // uncaught type error

var add = function (x, y) {
  return x + y;
};

add(3, 4); // 7
```

- 위 예제에서는 **호이스팅이 일어나지 않는다.**
- 때문에 함수 표현식만을 사용할 것을 권하고 있다.

# 2. 함수 객체 : 함수도 객체다

## 2-1. 자바스크립트에서는 함수도 객체다

자바스크립트에서는 **함수도 객체다.** 함수의 기본 기능인 코드 실행뿐만 아니라, 프로퍼티들을 가질 수 있다는 것이다.

```javascript
// 함수 선언 방식으로 add() 함수 정의
function add(x, y) {
  return x + y;
}

// add() 함수 객체에 result, status 프로퍼티 추가
add.result = add(3, 2);
add.status = "OK";

console.log(add.result); // 5
console.log(add.status); // 'OK'
```

## 2-2. 자바스크립트에서 함수는 값으로 취급된다

이는 **함수도 일반 객체처럼 취급될 수 있다**는 것이다. 자바스크립트 함수는 다음과 같은 동작이 가능하다.

- 리터럴에 의해 생성
- 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능
- 함수의 인자로 전달 가능
- 함수의 리턴값으로 리턴 가능
- 동적으로 프로퍼티를 생성 및 할당 가능

이와 같은 특징이 있으므로 자바스크립트에서는 함수를 **일급 객체**라고 부른다. 앞에서 나열한 기능이 모두 가능한 객체를 일급 객체라고 부르는 데, 자바스크립트 함수는 이러한 특성으로 함수형 프로그래밍이 가능하다. 따라서 함수를 변수나 객체, 배열 등에 값으로 저장할 수도 있으며, 다른 함수의 인자로 전달한다거나 함수의 리턴값으로도 사용 가능하다는 것을 이해해야 한다.

### 2-2-1. 변수나 프로퍼티의 값으로 할당

함수는 숫자나 문자열처럼 변수나 프로퍼티의 값으로 할당될 수 있다.

```javascript
// 변수에 함수 할당
var foo = 100;
var bar = function () {
  return 100;
};
console.log(bar()); // 100

// 프로퍼티에 함수 할당
var obj = {};
obj.baz = function () {
  return 200;
};
console.log(obj.baz()); // 200
```

### 2-2-2. 함수 인자로 전달

함수는 다른 함수의 인자로도 전달이 가능하다.

```javascript
// 함수 표현식으로 foo() 함수 생성
var foo = function (func) {
  func(); // 인자로 받은 func() 함수 호출
};

// foo() 함수 실행
foo(function () {
  console.log("argument"); // argument
});
```

### 2-2-3. 리턴값으로 활용

함수는 다른 함수의 리턴값으로 활용할 수 있다.

```javascript
// 함수를 리턴하는 foo() 함수 정의
var foo = function () {
  return function () {
    console.log("return value");
  };
};

var bar = foo();
bar(); // return value
```

## 2-3. 함수 객체의 기본 프로퍼티

- 함수는 일반적인 객체의 기능에 추가로 호출됐을 때 정의된 코드를 실행하는 기능을 가지고 있다.
- 일반 객체와는 다르게 추가로 **함수 객체만의 표준 프로퍼티**가 정의되어 있다.
- ECMA5 스크립트 명세서에는 모든 함수가 **length**와 **prototype 프로퍼티**를 가져야 한다고 기술하고 있다.
- **name 프로퍼티**는 함수의 이름을 나타낸다.
- **caller 프로퍼티**는 자신을 호출한 함수를 나타낸다.
- **arguments 프로퍼티**는 함수를 호출할 때 전달된 인자값을 나타낸다.
- 함수 객체의 부모 역할을 하는 프로토타입 객체를 **Function.prototype 객체**라고 하며, **함수 객체**라고 정의하고 있다.

### 2-3-1. length 프로퍼티

함수 객체의 **length 프로퍼티**는 모든 함수가 가져야 하는 표준 프로퍼티로서, 함수가 정상적으로 실행될 때 기대되는 인자의 개수를 나타낸다.

```javascript
function func0() {}
function func1(x) {
  return x;
}
function func2(x, y) {
  return x + y;
}
function func3(x, y, z) {
  return x + y + z;
}
console.log("func0.length - " + func0.length); // func0.length - 0
console.log("func1.length - " + func1.length); // func0.length - 1
console.log("func2.length - " + func2.length); // func0.length - 2
console.log("func3.length - " + func3.length); // func0.length - 3
```
