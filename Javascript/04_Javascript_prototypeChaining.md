# 5. 프로토타입 체이닝

## 5-1. 프로토타입의 두 가지 의미

- 자바스크립트는 **프로토타입 기반의 객체지향 프로그래밍**을 지원한다.
- 후에 알아 볼 OOP 상속에 근간이 되는 **프로토타입**과 **프로토타입 체이닝**을 알아볼 것이다.
- 자바스크립트에서는 클래스 개념이 없어서 객체 리터럴이나 생성자 함수로 객체를 생성한다.
- 모든 객체는 자신의 부모인 프로토 타입 객체를 가리키는 **[[Prototype]]링크**를 가진다.
- 모든 객체는 자신을 생성한 생성자 함수의 **prototype 프로퍼티**가 가리키는 **프로토타입 객체**를 자신의 부모 객체로 설정하는 **[[Prototype]]링크**로 연결한다.

```javascript
function Person(name) {
  this.name = name;
}

var foo = new Person("foo");

console.log(Person);
console.log(foo);
```

- 1. Person() 생성자 함수는 prototype 프로퍼티로 자신과 링크된 **프로토타입 객체**를 가리킨다.
- 2. 자바스크립트에서 객체를 생성하는 건 생성자 함수지만, 객체의 실제 부모 역할을 하는 건 생성자의 프로토타입 객체다.
- 3. 결과값을 보면 Person()와 foo 객체가 같은 프로토타입 객체를 가진 것을 볼 수 있다.
- 4. proto 프로퍼티나 [[Prototype]] 프로퍼티는 같다고 간주하면 된다.

## 5-2. 객체 리터럴 방식으로 생성된 객체의 프로토타입 체이닝

자바스크립트의 객체는 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티를 자신의 것처럼 접근하는 게 가능한 데, 이것이 **프로토타입 체이닝**이다.

```javascript
// 객체 리터럴 방식에서의 프로토타입 체이닝
var obj = {
  name: "foo",
  sayName: function () {
    console.log("My name is" + this.name);
  },
};

obj.sayName(); // My name is foo
console.log(obj.hasOwnProperty("name")); // true
console.log(obj.hasOwnProperty("nickName")); // false
obj.sayNickName(); // Uncaught TypeError
```

- 1. sayName() 메서드의 결과값은 출력됐지만, sayNickName() 메서드는 obj의 메서드가 아니므로 에러가 발생한다.
- 2. **[hasOwnProperty()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)** 메서드는 호출한 객체에 인자로 넘긴 문자열 이름의 프로퍼티나 메서드가 있는지 체크하는 자바스크립트 표준 API 함수다.
- 3. 특정 객체의 프로퍼티나 메서드에 접근하려고 할 때, 해당 객체에 접근하려는 프로퍼티나 메서드가 없다면 **[[Prototype]]링크**를 따라 부모 역할을 하는 프로토타입 객체의 프로퍼티를 차례대로 검색하는 것을 **프로토타입 체이닝**이라고 한다.

## 5-3. 생성자 함수로 생성된 객체의 프로토타입 체이닝

"자바스크립트에서 모든 **객체**는 자신을 생성한 **생성자 함수**의 **prototype 프로퍼티가 가리키는 객체**를 자신의 **프로토타입 객체**로 취급한다."

```javascript
// 생성자 함수 방식에서의 프로토타입 체이닝
function Person(name, age) {
  this.name = name;
  this.age = age;
}

var foo = new Person("foo", 30);

console.log(foo.hasOwnProperty("name")); // true
console.dir(Person.prototype);
```

- 1. foo 객체의 프로토타입 객체는 Person.prototype이다.
- 2. 함수에 연결된 프로토타입 객체는 디폴트로 **constructor 프로퍼티**만을 가진 객체이므로 hasOwnProperty() 메서드는 없다.
- 3. 프로토타입 체이닝은 Object.prototype 객체로 계속 이어져 true가 출력된다.

## 5-4. 프로토타입 체이닝의 종점

- 자바스크립트에서 Object.prototype 객체는 **프로토타입 체이닝의 종점**이다.
- 객체 리터럴 방식이나 생성자 함수 방식에 상관없이 모든 자바스크립트 객체는 Object.prototype 객체가 가진 프로퍼티와 메서드에 접근하고, 공유가 가능하다.

## 5-5. 기본 데이터 타입 확장

- Object.prototype에 정의된 메서드들은 자바스크립트의 모든 객체의 표준 메서드라고 볼 수 있다.
- 숫자, 문자열, 배열 등에서 사용되는 표준 메서드들의 경우, **Number.prototype**, **String.prototype**, **Array.prototype** 등에 정의되어 있다.
- 이러한 기본 내장 프로토타입 객체 또한 **Object.prototype**을 프로토타입으로 가지고 있어서 프로토타입 체이닝으로 연결된다.

```javascript
// String 기본 타입에 메서드 추가
String.prototype.testMethod = function () {
  console.log(String.prototype.testMethod());
};

var str = "Test";
str.testMethod();

console.dir(String.prototype);
```

**String.prototype**에 testMethod()를 추가하여 이후 문자열에서는 testMethod()를 문자열 API처럼 사용할 수 있다.

## 5-6. 프로토타입도 자바스크립트 객체다

- 함수가 생성될 때, 자신의 prototype 프로퍼티에 연결되는 프로토타입 객체는 디폴트로 constructor 프로퍼티만을 가진 객체다.
- **프로토타입 객체 역시 자바스크립트 객체**이므로 일반 객체처럼 동적으로 프로퍼티를 추가/삭제하는 것이 가능하다.
- 이렇게 변경된 프로퍼티는 실시간으로 프로토타입 체이닝에 반영된다.

```javascript
function Person(name) {
  this.name = name;
}

var foo = new Person("foo");

foo.sayHello(); // 에러

Person.prototype.sayHello = function () {
  console.log("HELLO");
};

foo.sayHello(); // HELLO
```

## 5-7. 프로토타입 메서드와 this 바인딩

- 프로토타입 객체는 메서드를 가질 수 있다.
- 프로토타입 메서드 내부에서 this를 사용한다면 this는 그 메서드를 호출한 객체에 바인딩된다.

```javascript
// 프로토타입 메서드와 this 바인딩
function Person(name) {
  this.name = name;
}

Person.prototype.getName() = function () {
  return this.name;
};

var foo = new Person("foo");

console.log(foo.getName()); // foo

Person.prototype.name = "person";

console.log(Person.prototype.getName()); // person
```

## 5-8. 디폴트 프로토타입은 다른 객체로 변경이 가능하다

- 디폴트 프로토타입 객체는 함수가 생성될 때 같이 생성되며, 함수의 prototype 프로퍼티에 연결된다.
- 자바스크립트에서는 **디폴트 프로토타입 객체를 다른 일반 객체로 변경하는 것이 가능하다.**
- 이러한 특징을 이용해서 객체지향의 상속을 구현한다.
- 생성자 함수의 프로토타입 객체가 변경되면, 이후에 생성된 객체들은 변경된 프로토타입 객체로 [[Prototype]]링크를 연결한다.

```javascript
// 프로토타입 객체 변경
function Person(name) {
  this.name = name;
}
console.log(Person.prototype.constructor); // Person(name)

var foo = new Person("foo");
console.log(foo.country); // undefined

Person.prototype = {
  country: "korea",
};
console.log(Person.prototype.constructor); // Object()

var bar = new Person("bar");
console.log(foo.country); // undefined
console.log(bar.country); // korea
console.log(foo.constructor); // Person(name)
console.log(bar.constructor); // Object()
```

- 1. Person.prototype.constructor는 Person() 생성자 함수를 가리킨다.
- 2. foo 객체는 Person.prototype 객체를 프로토타입으로 연결한다. foo 객체와 Person.prototype은 country 프로퍼티가 없으므로 undefined 값이 출력된다.
- 3. 객체 리터럴 방식으로 생성한 country 프로퍼티를 가진 객체로 프로토타입 객체를 변경했다.
- 4. 변경한 프로토타입 객체는 country 프로퍼티가 있으므로, 디폴트 프로토타입 객체처럼 **constructor 프로퍼티가 없다.**
- 5. 변경한 프로토타입 객체는 객체 리터럴 방식으로 생성했으므로 **Object.prototype**을 [[Prototype]]으로 연결하고, Object.prototype 역시 Object() 생성자 함수와 연결된 프로토타입 객체여서, Object() 생성자 함수를 constructor 프로퍼티에 연결하고 있다.
- 6. bar 객체는 새로 변경된 프로토타입 객체를 [[Prototype]]링크로 가리키게 된다.
- 7. foo 객체는 디폴트 프로토타입 객체를, bar 객체는 새로 변경된 프로토타입 객체를 연결해서, 서로 다른 결과값을 만들어 버린다.

## 5-9. 객체의 프로퍼티 읽기나 메서드를 실행할 때만 프로토타입 체이닝이 동작한다

자바스크립트는 객체에 없는 프로퍼티에 값을 쓰려고 할 경우 동적으로 객체에 프로퍼티를 추가한다.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.country = "Korea";

var foo = new Person("foo");
var bar = new Person("bar");
console.log(foo.country); // Korea
console.log(bar.country); // Korea
foo.country = "USA";

console.log(foo.country); // USA
console.log(bar.country); // Korea
```
