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

#### 2-1-3. 생성자 함수 이용

- 함수를 통해서도 객체를 생성할 수 있으며 이렇게 객체를 생성하는 함수를 생성자 함수라고 부른다.

### 2.2 객체 프로퍼티 읽기/쓰기/갱신

- 객체의 프로퍼티에 접근하려면 다음과 같이 두 가지 방법을 사용한다.
  - 대괄호 [] 표기법
  - 마침표 . 표기법

```javascript
// 객체 리터럴 방식을 통한 foo 객체 생성
var foo = {
  name: "foo",
  major: "computer science",
};

// 객체 프로퍼티 읽기
console.log(foo.name); // foo
console.log(foo["name"]); // foo
console.log(foo.nickname); // undefined

// 객체 프로퍼티 갱신
foo.major = "electronics engineering";
console.log(foo.major); // electronics engineering
console.log(foo["major"]); // electronics engineering

// 객체 프로퍼티 동적 생성
foo.age = 30;
console.log(foo.age); // 30

// 대괄호 표기법만을 사용해야 할 경우
foo["full-name"] = "foo bar";
console.log(foo["full-name"]); // foo bar
console.log(foo.full - name); // NaN
console.log(foo.full); // undefined
console.log(name); // undefined
```

#### 2-2-1. 프로퍼티 읽기

- 대괄호 표기법에서는 접근하려는 프로퍼티 이름을 문자열 형태로 만들어야 한다.
- foo['name'] 대신에 foo[name]이라고 접근하면 undefined 값이 출력된다.
- 자바스크립트에서는 대괄호 표기법에서 접근하려는 프로퍼티 이름을 문자열 형태로 만들지 않으면 _toString()_ 이라는 메서드를 자동으로 호출해서 이를 문자열로 바꾸려는 시도를 한다. 객체에 없는 프로퍼티에 접근하는 경우는 undefined 값이 출력된다.

#### 2-2-2. 프로퍼티 갱신

- 프로퍼티에 접근해서 객체의 기존 프로퍼티 값을 갱신할 수 있다.

#### 2-2-3. 프로퍼티 동적 생성

- 객체가 생성된 후에도 동적으로 프로퍼티를 생성해서 해당 객체에 추가할 수 있다.
- **자바스크립트 객체의 프로퍼티에 값을 할당할 때, 프로퍼티가 이미 있을 경우는 해당 프로퍼티의 값이 갱신되지만, 객체의 해당 프로퍼티가 없을 경우에는 새로운 프로퍼티가 동적으로 생성된 후 값이 할당된다.**

#### 2-2-4. 대괄호 표기법만을 사용해야 할 경우

- 일반적으로 마침표 표기법을 주로 사용한다.
- 접근하려는 프로퍼티가 표현식이거나 예약어일 경우에는 대괄호 표기법만을 이용해서 접근해야 한다.
- 'full-name' 프로퍼티의 경우는 '-' 연산자가 있는 표현식이라 대괄호 표기법을 이용해서 접근해야 한다.
- 자바스크립트에서 수치 연산을 해서 정상적인 값을 얻지 못할 때 **NaN** 값이 출력된다.

### 2-3. for in 문과 객체 프로퍼티 출력

for in 문을 사용하면, 객체에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다.

```javascript
// 객체 리터럴을 통한 foo 객체 생성
var foo = {
  name: "foo",
  age: 30,
  major: "computer science",
};

// for in 문을 이용한 객체 프로퍼티 출력
var prop;
for (prop in foo) {
  console.log(prop, foo[prop]);
} // name foo age 30 major 'computer science'
```

### 2-4. 객체 프로퍼티 삭제

객체의 프로퍼티를 delete 연산자를 이용해 즉시 삭제할 수 있다. 주의할 점은 delete 연산자는 객체의 프로퍼티를 삭제할 뿐, 객체 자체를 삭제하지는 못한다는 것이다.

```javascript
// 객체 리터럴을 통한 foo 객체 생성
var foo = {
  name: "foo",
  nickname: "babo",
};

console.log(foo.nickname); // babo
delete foo.nickname; // nickname 프로퍼티 삭제
console.log(foo.nickname); // undefined

delete foo; // foo 객체 삭제 시도
console.log(foo.name); // foo
```

## 3. 참조 타입의 특성

자바스크립트에서는 기본 타입인 number, string, boolean, null, undefined 5가지를 제외한 모든 값은 객체다.  
배열이나 함수 또한 객체로 취급된다. 이러한 객체는 자바스크립트에서는 참조 타입이라고 부른다. 이것은 객체의 모든 연산이 실제 값이 아닌 참조값으로 처리되기 때문이다.

```javascript
var objA = {
  val: 40,
};
var objB = objA;

console.log(objA.val); // 40
console.log(objB.val); // 40

objB.val = 50;
console.log(objA.val); // 50
console.log(objB.val); // 50
```

- objA 변수는 객체 자체를 저장하고 있는 것이 아니라 생성된 객체를 가리키는 참조값을 저장하고 있다.
- 변수 objB에 objA 값을 할당한다. objA와 objB 변수가 동일한 객체를 가리키는 참조값을 가지게 되는 것이다. 때문에 값이 40으로 같다.
- 변수 objB가 가리키는 객체의 val 값을 50으로 갱신했을때 objA의 값도 50으로 변경된다.

### 3.1 객체 비교

동등 연산자(==)를 사용하여 두 객체를 비교할 때도 객체의 프로퍼티 값이 아닌 참조값을 비교한다는 것에 주의해야 한다.

```javascript
var a = 100;
var b = 100;

var objA = { value: 100 };
var objB = { value: 100 };
var objC = objB;

console.log(a == b); // true
console.log(objA == objB); // false
console.log(objB == objC); //true
```

- a와 b는 숫자 100을 저장하고 있는 기본 타입의 변수다. 기본 타입의 경우 동등 연산자를 이용해 비교할 때 값을 비교한다.
- objA와 objB는 다른 객체지만 같은 형태의 프로퍼티 값을 가지고 있다. 객체와 같은 참조 타입의 경우는 **참조값이 같아야 true**가 된다.

### 3.2 참조에 의한 함수 호출 방식

기본 타입과 참조 타입의 경우는 함수 호출 방식도 다르다. 기본 타입의 경우는 **값에 의한 호출 방식**으로 동작한다. 즉, 함수를 호출할 때 인자로 기본 타입의 값을 넘길 경우, 호출된 함수의 매개변수로 **복사한 값**이 전달된다. 때문에 함수 내부에서 매개변수를 이용해 값을 변경해도, 실제로 호출된 변수의 값이 변경되지는 않는다.

이에 반해 객체와 같은 참조 타입의 경우 함수를 호출할 때 **참조에 의한 호출 방식**으로 동작한다. 즉, 함수를 호출할 때 인자로 참조 타입인 객체를 전달할 경우, 객체의 프로퍼티 값이 함수의 매개변수로 복사되지 않고, 인자로 넘긴 객체의 참조값이 그대로 함수 내부로 전달된다. 때문에 함수 내부에서 참조값을 이용해서 인자로 넘긴 실제 객체의 값을 변경할 수 있는 것이다.

```javascript
var a = 100;
var objA = { value: 100 };

function changeArg(num, obj) {
  num = 200;
  obj.value = 200;

  console.log(num);
  console.log(obj);
}

changeArg(a, objA); // 200 { value: 200 }

console.log(a); // 100
console.log(objA); // { value: 200 }
```

## 4. 프로토타입

자바스크립트의 **모든 객체는 자신의 부모 역할을 하는 객체와 연결되어 있다.** 이것은 객체지향의 상속 개념과 같이 부모 객체의 프로퍼티를 마치 자신의 것처럼 쓸 수 있는 것 같은 특징이 있다. 자바스크립트에서는 이러한 부모 객체를 **프로토타입 객체**라고 부른다.

```javascript
var foo = {
  name: "foo",
  age: 30,
};

console.log(foo.toString()); // 01
console.dir(foo); // 02
```

- **foo 객체의 프로토타입**에 toString() 메서드가 이미 정의되어 있고, foo 객체가 상속처럼 toString() 메서드를 호출해서 에러가 없다.
- 개발자 도구에서 객체를 출력해보면 ***proto*프로퍼티**가 있는데 이 프로퍼티가 **프로토타입 객체**를 가리킨다.

자바스크립트의 **모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]]라는 숨겨진 프로퍼티**를 가진다. 크롬 브라우저에서는 *proto*를 의미한다. 모든 객체의 프로토타입은 자바스크립트의 룰에 따라 객체를 생성할 때 결정된다. 우선은 객체 리터럴 방식으로 생성된 객체의 경우 **Object.prototype 객체**가 프로토타입 객체가 된다는 것만 기억하고 넘어가자.

참고로 _proto_ 프로퍼티가 가리키는 객체가 바로 Object.Prototype 이며, toString(), valueOf() 등과 같은 모든 객체에서 호출 가능한 자바스크립트 기본 내장 메서드가 포함되어 있다. 그 결과 foo 객체는 foo.toString()과 같이 자신의 프로토타입인 Object.prototype 객체에 포함된 다양한 메서드를 마치 자신의 프로퍼티인 것처럼 상속받아 사용할 수 있다.
