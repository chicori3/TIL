### 4. 함수 호출과 this

### 4-1. arguments 객체

자바스크립트에서는 함수를 호출할 때 함수 형식에 맞춰 인자를 넘기지 않더라도 에러가 발생하지 않는다. 이러한 특성 때문에 함수 코드를 작성할 때, 런타임 시에 호출된 인자의 개수를 확인하고 이에 따라 동작을 다르게 해줘야 할 경우가 있다. 이를 가능케 하는 게 **arguments 객체**다. 자바스크립트에서는 함수를 호출할 때 인수들과 함께 arguments 객체가 함수 내부로 전달된다. arguments 객체는 함수를 호출할 때 넘긴 인자들이 **유사 배열 형태로 저장된 객체**이다. 매개변수 개수가 정확하게 정해지지 않은 함수를 구현하거나, 전달된 인자의 개수에 따라 서로 다른 처리를 해줘야 하는 함수를 개발하는 데 유용하게 사용할 수 있다.

```javascript
function sum() {
  var result = 0;

  for (var i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
}

console.log(sum(1, 2, 3)); // 6
console.log(sum(1, 2, 3, 4, 5, 6)); // 21
```

### 4-2. 호출 패턴과 this 바인딩

자바스크립트에서 함수를 호출할 때 arguments 객체 및 **this 인자**가 함수 내부로 전달된다. this는 핵심 개념이면서 이해하기 어려운데, **함수가 호출되는 방식**에 따라 this가 다른 **객체를 참조(this 바인딩)** 때문이다.

#### 4-2-1. 객체의 메서드 호출할 때 this 바인딩

객체의 프로퍼티가 함수일 경우, 이 함수를 메서드라고 부른다. 메서드를 호출할 때, 메서드 내부 코드에서 사용된 this는 **해당 메서드를 호출한 객체로 바인딩**된다.

```javascript
var myObj = {
  name: "foo",
  sayName: function () {
    console.log(this.name);
  },
};

var otherObj = {
  name: "bar",
};

otherObj.sayName = myObj.sayName;

myObj.sayName(); // foo
otherObj.sayName(); // bar
```

#### 4-2-2. 함수를 호출할 때 this 바인딩

자바스크립트에서는 함수를 호출하면, 해당 함수 내부 코드에서 사용된 **this는 전역 객체에 바인딩**된다. 브라우저에서 자바스크립트를 실행하는 경우 전역 객체는 **window 객체**가 된다.

```javascript
// 함수를 호출할 때 this 바인딩
var test = "This is test";
console.log(window.test); // This is test

var sayFoo = function () {
  console.log(this.test);
};

sayFoo(); // This is test
```

이러한 함수 호출에서의 this 바인딩 특성은 **내부 함수를 호출했을 경우**에도 그대로 적용되므로 주의해야 한다.

```javascript
// 내부 함수의 this 바인딩
var value = 100;

var myObject = {
  value: 1,
  func1: function () {
    this.value += 1;
    console.log(this.value);

    func2 = function () {
      this.value += 1;
      console.log(this.value);

      func3 = function () {
        this.value += 1;
        console.log(this.value);
      };
      func3();
    };
    func2();
  },
};

myObject.func1(); // 1 101 102
```

예상대로라면 결과는 2, 3, 4로 나타났을 테지만, 다른 이유는 자바스크립트에서는 **내부 함수 호출 패턴을 정의해 놓지 않기 때문이다.**
내부 함수도 결국 함수이므로 이를 호출할 때는 함수 호출로 취급된다. 따라서 내부 함수의 this는 전역 객체(window)에 바인딩된다. 때문에 window.value 값에 1을 더한 결과가 나오게 된다. 이렇게 내부 함수가 this를 참조하는 자바스크립트의 한계를 극복하려면 **부모 함수**를 내부 함수가 접근 가능한 **다른 변수에 저장**하는 방법이 사용된다.

```javascript
// 내부 함수의 this 바인딩 문제를 해결하는 방법
var value = 100;

var myObject = {
  value: 1,
  func1: function () {
    var that = this;
    this.value += 1;
    console.log(this.value);

    func2 = function () {
      that.value += 1;
      console.log(that.value);

      func3 = function () {
        that.value += 1;
        console.log(that.value);
      };
      func3();
    };
    func2();
  },
};

myObject.func1(); // 2 3 4
```

#### 4-2-3. 생성자 함수를 호출할 때 this 바인딩

자바와 같은 객체지향 언어에서의 생성자 함수의 형식과는 다르게 **기존 함수에 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작한다.** 반대로 일반 함수에 new를 붙여 호출하면 원치 않는 생성자 함수처럼 동작할 수 있다. 따라서 대부분의 자바스크립트 스타일 가이드에서는 특정 함수가 생성자 함수로 정의되어 있음을 알리기 위해 **함수 이름의 첫 문자를 대문자로 쓰기**를 권하고 있다. 생성자 함수 코드 내부에서 this는 다르게 동작한다.

_new 연산자로 함수를 생성자로 호출했을 때_

- 생성자 함수 코드가 실행되기 전 **빈 객체**가 생성된다. 이 객체는 this로 바인딩되며 **생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토타입 객체**로 설정한다.
- 이후에는 함수 코드 내부에서 this를 사용해서 동적으로 프로퍼티나 메서드를 생성할 수 있다.
- 특별하게 리턴문이 없을 경우, **this로 바인딩된 새로 생성된 객체가 리턴**된다. 이는 뒤에서 더 자세히 알아볼 것이다.

```javascript
// 생성자 함수의 동작 방식
var Person = function (name) {
  this.name = name;
};

var foo = new Person("foo");
console.log(foo.name); // foo
```

_객체 리터럴 방식과 생성자 함수를 통한 객체 생성 방식의 차이_

- 객체 리터럴 방식으로 생성된 객체는 같은 형태의 객체를 재생성할 수 없다.
- 생성자 함수를 사용해서 객체를 생성한다면, 생성자 함수를 호출할 때 다른 인자를 넘김으로써 같은 형태의 다른 객체를 생성할 수 있다.
- **프로토타입 객체**가 다른데, 객체 리터럴 방식은 **Object**, 생성자 함수 방식의 경우는 **Person**으로 서로 다르다.
- 객체는 자신을 생성한 **생성자 함수의 prototype 프로퍼티**가 가리키는 객체를 자신의 **프로토타입 객체**로 설정한다.
- 객체 리터럴 방식의 객체 생성자 함수는 **Object()** 이며 생성자 함수 방식의 경우는 **생성자 함수** 자체이다.

_생성자 함수를 new를 붙이지 않고 호출할 경우_

객체 생성을 목적으로 작성한 생성자 함수를 new 없이 호출하거나 일반 함수를 new를 붙여 호출할 경우 오류가 발생할 수 있다. 그 이유는 일반 함수 호출과 생성자 함수를 호출할 때 this 바인딩 방식이 다르기 때문이다.

```javascript
// new를 붙이지 않은 생성자 함수 호출의 오류
var qux = Person("qux", 20);
console.log(qux); // undefined

console.log(window.name); // qux
console.log(window.age); // 20
```

new 없이 일반 함수 형태로 호출할 경우, this는 함수 호출이므로 전역 객체인 window 객체로 바인딩된다. Person 객체를 생성해서 qux 변수에 저장하려는 의도와는 다르게 this가 바인딩된 **window 객체에 동적으로 프로퍼티가 생성**된 것이다.

_강제로 인스턴스 생성하기_

```javascript
function A(arg) {
  if (!(this instanceof A)) return new A(arg);
  this.value = arg ? arg : 0;
}

var a = new A(100);
var b = A(10);

console.log(a.value); // 100
console.log(b.value); // 10
console.log(global.value); // undefined
```

함수 A에서는 A가 호출될 때, this가 A의 인스턴스인지 확인하는 분기문이 추가되었다. this가 A의 인스턴스가 아니라면, new로 호출된 것이 아님을 의미하고, new로 A를 호출하여 반환하게 하였다. 이렇게 하면 var b = A(10);과 같이 사용자가 사용했다고 하더라도, 전역 객체에 접근하지 않고, 새 인스턴스가 생성되어 b에 반환될 것이다. 이와 같이 하면, 특정 함수 이름과 상관없이 이 패턴을 공통으로 사용하는 모듈을 작성할 수 있는 장점이 있다.

#### 4-2-4. call과 apply 메서드를 이용한 명시적인 this 바인딩

- 자바스크립트는 내부적인 this 바인딩 이외에도 특정 객체에 **명시적으로 바인딩** 시키는 방법도 제공한다.
- 이를 가능케 하는 것이 **[apply()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)** 와 **[call()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call)** 메서드다.
- apply() 메서드는 this를 특정 객체에 바인딩할 뿐 본질적인 기능은 **함수 호출**이다.
- apply()나 call() 메서드는 this를 명시적으로 매핑해서 특정 함수나 메서드를 호출할 수 있다는 장점이 있다.
- 대표적인 용도가 앞서 설명한 arguments 객체와 같은 **유사 배열 객체에서 배열 메서드를 사용**하는 경우이다.

```javascript
// apply() 메서드를 이용한 this 바인딩
function Person(name, age) {
  this.name = name;
  this.age = age;
}

var foo = {};

Person.apply(foo, ["foo", 30]);
console.dir(foo);
```

```javascript
// apply() 메서드를 활용한 arguemnts 객체의 slice() 활용
function myFunction() {
  console.dir(arguments);

  arguments.shift(); // 에러 발생

  var args = Array.prototype.slice.apply(arguments);
  console.dir(args);
}

myFunction(1, 2, 3);
```

1.  배열에서는 [shift()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) 메서드를 사용해 첫 번째 원소를 쉽게 삭제할 수 있지만, arguments 객체는 유사 객체 배열이므로 에러가 발생한다.
2.  Array.prototype.slice() 메서드를 호출하고 this는 arguments 객체로 바인딩시킨다.

### 4-3. 함수 리턴

- **자바스크립트 함수는 항상 리턴값을 반환한다.** return 문을 사용하지 않았더라도 다음의 규칙으로 전달한다.

#### 4-3-1. 규칙 1) 일반 함수나 메서드는 리턴값을 지정하지 않을 경우, undefined 값이 리턴된다

```javascript
// return 문 없는 일반 함수
var noReturn = function () {
  console.log("No return");
};

var result = noReturn();
console.log(result); // No return undefined
```

#### 4-3-2. 규칙 2) 생성자 함수에서 리턴값을 지정하지 않을 경우 생성된 객체가 리턴된다

```javascript
// 생성자 함수에서 명시적으로 객체를 리턴
function Person(name, age) {
  this.name = name;
  this.age = age;

  return { name: "bar", age: 20 };
}

var foo = new Person("foo", 30);
console.log(foo); // age: 20 name: bar
```

생성자 함수의 리턴값으로 넘긴 값이 객체가 아닌 불린, 숫자, 문자열의 경우는 this로 바인딩된 객체가 리턴된다.

```javascript
// 생성자 함수에서 명시적으로 기본 타입값을 리턴
function Person(name, age) {
  this.name = name;
  this.age = age;

  return 100;
}

var foo = new Person("foo", 30);
console.log(foo); // Person {name: "foo", age: 30}
```
