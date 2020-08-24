# 04. 함수와 프로토타입 체이닝

자바스크립트에서 가장 중요한 개념 1순위는 당연 **함수**다. 자바스크립트에서의 함수는 언뜻 보면 여느 언어와 마찬가지의 기능을 제공한다.

## 1. 함수 정의

- 함수 선언문
- 함수 표현식
- Function() 생성자 함수

### 1-1. 함수 리터럴

- 자바스크립트에서 함수는 일반 객체처럼 값으로 취급된다.
- **함수 리터럴**을 이용해 함수 생성

```javascript
function name(arg) {
  return x + y;
}
```

### 1-2. 함수 선언문 방식으로 함수 생성하기

함수 선언문 방식으로 정의된 함수의 경우는 **반드시 함수명이 정의되어 있어야 한다**.

```javascript
// add() 함수 선언문
function add(x, y) {
  return x + y;
}

console.log(add(3, 4)); // 7
```

### 1-3. 함수 표현식 방식으로 함수 생성하기

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

### 1-4. Function() 생성자 함수를 통한 함수 생성하기

- 자바스크립트의 함수도 **Function()** 이라는 기본 내장 생성자 함수로부터 생성된 **객체**이다.
- 함수 선언문, 함수 표현식 방식도 결국엔 내부적으로는 Function() 생성자 함수로 함수가 생성된다고 볼 수 있다.
- 일반적으로 사용되지 않으니 알아만 두자.

```javascript
// Function() 생성자 함수 이용
var add = new Function("x", "y", "return x+y");
console.log(add(3, 4)); // 7
```

### 1-5. 함수 호이스팅

```javascript
// 함수 선언문 방식
add(2, 3); // 5

function add(x, y) {
  return x + y;
}

add(3, 4); // 7
```

- 위 예제에서 add() 함수가 정의되지 않았음에도 함수를 호출하는 것이 가능한 데, **함수 선언문 형태로 정의한 함수의 유효 범위는 코드의 맨 처음부터 시작한다**는 것을 확인할 수 있다.
- **[함수 호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)** 은 자바스크립트의 **변수 생성**과 **초기화**의 작업이 분리되어 진행되기 때문에 발생한다.

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

## 2. 함수 객체 : 함수도 객체다

### 2-1. 자바스크립트에서는 함수도 객체다

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

### 2-2. 자바스크립트에서 함수는 값으로 취급된다

이는 **함수도 일반 객체처럼 취급될 수 있다**는 것이다. 자바스크립트 함수는 다음과 같은 동작이 가능하다.

- 리터럴에 의해 생성
- 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능
- 함수의 인자로 전달 가능
- 함수의 리턴값으로 리턴 가능
- 동적으로 프로퍼티를 생성 및 할당 가능

이와 같은 특징이 있으므로 자바스크립트에서는 함수를 **일급 객체**라고 부른다. 앞에서 나열한 기능이 모두 가능한 객체를 일급 객체라고 부르는 데, 자바스크립트 함수는 이러한 특성으로 함수형 프로그래밍이 가능하다. 따라서 함수를 변수나 객체, 배열 등에 값으로 저장할 수도 있으며, 다른 함수의 인자로 전달한다거나 함수의 리턴값으로도 사용 가능하다는 것을 이해해야 한다.

#### 2-2-1. 변수나 프로퍼티의 값으로 할당

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

#### 2-2-2. 함수 인자로 전달

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

#### 2-2-3. 리턴값으로 활용

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

### 2-3. 함수 객체의 기본 프로퍼티

- 함수는 일반적인 객체의 기능에 추가로 호출됐을 때 정의된 코드를 실행하는 기능을 가지고 있다.
- 일반 객체와는 다르게 추가로 **함수 객체만의 표준 프로퍼티**가 정의되어 있다.
- ECMA5 스크립트 명세서에는 모든 함수가 **length**와 **prototype 프로퍼티**를 가져야 한다고 기술하고 있다.
- **name 프로퍼티**는 함수의 이름을 나타낸다.
- **caller 프로퍼티**는 자신을 호출한 함수를 나타낸다.
- **arguments 프로퍼티**는 함수를 호출할 때 전달된 인자값을 나타낸다.
- 함수 객체의 부모 역할을 하는 프로토타입 객체를 **Function.prototype 객체**라고 하며, **함수 객체**라고 정의하고 있다.

#### 2-3-1. length 프로퍼티

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

#### 2-3-2. prototype 프로퍼티

모든 함수는 객체로서 **prototype 프로퍼티**를 가지고 있는데 모든 객체의 부모를 나타내는 [[Prototype]]과 혼동하면 안된다. prototype 프로퍼티는 함수가 생성될 때 만들어지며 **constructor 프로퍼티** 하나만 있는 객체를 가리킨다. 즉, 자바스크립트에서는 함수를 생성할 때, 함수 자신과 연결된 프로토타입 객체를 동시에 생성하며, 이 둘은 각각 prototype과 constructor라는 프로퍼티로 서로를 참조하게 된다.

```javascript
function myFunction() {
  return true;
}

console.dir(myFunction.prototype);
console.dir(myFunction.prototype.constructor);
```

실행결과를 보면 myFunction.prototype 객체는 **constructor**와 **proto**라는 두 개의 프로퍼티가 있다. 이렇듯 **함수 객체**와 **프로토타입 객체**는 서로 밀접하게 연결돼 있다. 프로토타입과 프로토타입 체이닝을 이해하는 기본 지식인 만큼 잘 숙지해야한다.

## 3. 함수의 다양한 형태

### 3-1. 콜백 함수

자바스크립트 함수 표현식에서 **함수 이름**은 꼭 붙이지 않아도 되는 선택 사항이다. 이러한 익명 함수의 대표적인 용도가 **콜백 함수**이다. 콜백 함수는 코드를 통해 명시적으로 호출하는 함수가 아니라, 개발자는 단지 함수를 등록하기만 하고, 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 호출되는 함수를 말한다. 또한, 특정 함수의 인자로 넘겨서, 코드 내부에서 호출되는 함수 또한 콜백 함수가 될 수 있다. 대표적인 콜백 함수의 예가 이벤트 핸들러 처리이다.

```html
<!DOCTYPE html>
<html>
  <body>
    <script>
      // 페이지 로드 시 호출될 콜백 함수
      window.onload = function () {
        alert("Callback Function");
      };
    </script>
  </body>
</html>
```

window.onload는 이벤트 핸들러로서, 웹 페이지의 로딩이 끝나는 시점에 load 이벤트가 발생하면 실행된다.

### 3-2. 즉시 실행 함수

함수를 정의함과 동시에 바로 실행하는 함수를 **즉시 실행 함수**라고 한다.

```javascript
(function (name) {
  console.log("Immediate function -> " + name);
})("foo"); // Immediate function -> foo
```

즉시 실행 함수를 만드는 방법은 간단하다. 함수 리터럴을 ()로 둘러싸고 함수가 바로 호출될 수 있게 () 괄호 쌍을 추가한다. 이때 괄호 안에 값을 추가해 즉시 실행 함수의 인자로 넘길 수가 있다. 이렇게 함수가 선언되자마자 실행되게 만든 즉시 실행 함수의 경우, 같은 함수를 다시 호출할 수 없다. **최초 한 번의 실행만을 필요로 하는 초기화 코드 부분**등에 사용할 수 있다. jQuery와 같은 라이브러리나, 프레임워크 소스들에서 사용된다. jQuery에서 사용하는 이유는 자바스크립트의 변수 유효 범위 특성 때문인데, 자바스크립트에서는 **[함수 유효 범위](https://www.opentutorials.org/course/743/6495)** 를 지원한다. 기본적으로 변수를 선언할 경우 프로그램 전체에서 접근할 수 있는 전역 유효 범위를 가진다. 그러나 함수 내부에서 정의된 매개변수와 변수들은 함수 코드 내부에서만 유효할 뿐 함수 밖에서는 유효하지 않다. 함수 외부의 코드에서 함수 내부의 변수를 액세스하는 게 불가능하다는 것이다. 따라서 즉시 실행 함수 내에 라이브러리 코드를 추가하면 전역 네임스페이스를 더럽히지 않으므로, 이후 다른 라이브러리들이 동시에 로드가 되더라도 변수 이름 충돌 같은 문제를 방지할 수 있다.

### 3-3. 내부 함수

자바스크립트에서는 함수 코드 내부에서 함수 정의가 가능하다. 이것을 **내부 함수**라고 부른다. 내부 함수는 자바스크립트의 기능을 보다 강력하게 해주는 클로저를 생성하거나 부모 함수 코드에서 외부에서의 접근을 막고 독립적인 헬퍼 함수를 구현하는 용도 등으로 사용한다.

```javascript
function parent() {
  var a = 100;
  var b = 200;
  function child() {
    var b = 300;
    console.log(a); // 100
    console.log(b); // 300
  }
  child(); // Uncaught RefrenceError : child is not defined
}
```

- 내부 함수에서는 자신을 둘러싼 부모 함수의 변수에 접근이 가능하다. 이것이 가능한 이유는 **[스코프 체이닝](https://velog.io/@bathingape/%EC%8A%A4%EC%BD%94%ED%94%84Scope%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80Closure-%EC%9D%B4%ED%95%B4)** 때문이다.
- 내부 함수는 일반적으로 자신이 정의된 부모 함수 내부에서만 호출이 가능하다.
- 하지만 함수 외부에서도 특정 함수 스코프 안에 선언된 내부 함수를 호출할 수 있다.

```javascript
function parent() {
  var a = 100;
  var child = function () {
    console.log(a);
  };
}
return child;

var inner = parent();
inner(); // 100
```

이와 같이 실행이 끝난 parent()와 같은 부모 함수 스코프의 변수를 참조하는 inner()와 같은 함수를 **[클로저](https://velog.io/@bathingape/%EC%8A%A4%EC%BD%94%ED%94%84Scope%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80Closure-%EC%9D%B4%ED%95%B4)** 라고 한다.

### 3-4. 함수를 리턴하는 함수

함수를 호출함과 동시에 다른 함수로 바꾸거나, 자기 자신을 재정의하는 함수를 구현할 수 있다.

```javascript
var self = function () {
  console.log("a");
  return function () {
    console.log("b");
  };
};
self = self(); // a
self(); // b
```
