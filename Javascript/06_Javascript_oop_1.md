# 06. 객체지향 프로그래밍

자바스크립트는 여러 가지 특성으로 객체지향 언어의 특성을 구현해낼 수 있다. 객체지향 언어로서 클래스 기반의 언어와 프로토타입 기반의 언어를 간단하게나마 구분해서 알아야 할 필요가 있다.

- 클래스 기반의 언어는 클래스로 객체의 기본적인 형태와 기능을 정의하고, 생성자로 인스턴스를 만들어서 사용할 수 있다. 이런 유형의 언어는 모든 인스턴스가 클래스의 정의된 대로 같은 구조이고 보통 런타임에 바꿀 수 없다.
- 프로토타입 기반의 언어는 객체의 자료구조, 메서드 등을 동적으로 바꿀 수 있다.

## 1. 클래스, 생성자, 메서드

- 자바스크립트는 거의 모든 것이 객체이고, 특히 함수 객체로 많은 것을 구현해낸다.
- 클래스, 생성자, 메서드도 모두 함수로 구현이 가능하다.

```javascript
function Person(arg) {
  this.name = arg;

  this.getName = function () {
    return this.name;
  };
  this.setName = function (value) {
    this.name = value;
  };
}

var me = new Person("zzoon");
console.log(me.getName()); // zzoon

me.setName("iamhjoo");
console.log(me.getName()); // iamhjoo
```

- 자바스크립트에서 클래스 기반의 객체지향 프로그래밍은 기본적인 형태가 이와 같다.
- 클래스 및 생성자의 역할을 하는 함수가 있고, 사용자는 new 키워드로 인스턴스를 생성하여 사용할 수 있다.

```javascript
function Person(arg) {
  this.name = arg;
}

Person.prototype.getName = function () {
  return this.name;
};

Person.prototype.setName = function (value) {
  this.name = value;
};

var me = new Person("me");
var you = new Person("you");
console.log(me.getName());
console.log(you.getName());
```

- Person 함수 객체의 prototype 프로퍼티에 getName()과 setName() 함수를 정의하였다.
- 이 Person으로 객체를 생성하면 따로 함수 객체를 생성할 필요 없이 getName()과 setName() 함수를 프로토타입 체인으로 접근할 수 있다.
- 자바스크립트에서 클래스 안의 메서드를 정의할 때는 프로토타입 객체에 정의한 후, new로 생성한 객체에서 접근할 수 있게 하는 것이 좋다.

```javascript
Function.prototype.method = function (name, func) {
  if (!this.prototype[name]) this.prototype[name] = func;
};
```

## 2. 상속

- 자바스크립트는 클래스 기반의 상속을 지원하지 않는다.
- 객체 프로토타입 체인을 이용하여 상속을 구현해낼 수 있다.
- **프로토타입을 이용한 상속**은 객체 리터럴을 중심으로 철저히 프로토타입을 이용하여 상속을 구현해낸다.

### 2-1. 프로토타입을 이용한 상속

```javascript
function create_object(o) {
  function F() {
    F.prototype = o;
    return new F();
  }
}
```

1. create_object() 함수는 인자로 들어온 객체를 부모로 하는 자식 객체를 생성하여 반환한다.
2. 새로운 빈 함수 객체 F를 만들고, F.prototype 프로퍼티에 인자로 들어온 객체를 참조하여 함수 객체 F를 생성자로 하는 새로운 객체를 만들어 반환한다.
3. 이렇게 반환된 객체는 부모 객체의 프로퍼티에 접근할 수 있고, 자신만의 프로퍼티를 만들 수도 있다.

```javascript
var person = {
  name: "zzoon",
  getName: function () {
    return this.name;
  },
  setName: function (arg) {
    this.name = arg;
  },
};

function create_object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}

var student = create_object(person);

student.setName("me");
console.log(student.getName()); // me
```

```javascript
var person = {
  name: "white",
  getName: function () {
    return this.name;
  },
  setName: function () {
    this.name = arg;
  },
};

function create_object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}

function extend(obj, prop) {
  if (!prop) {
    prop = obj;
    obj = this;
  }
  for (var i in prop) obj[i] = prop[i];
  return obj;
}

var student = create_object(person);
var added = {
  setAge: function (age) {
    this.age = age;
  },
  getAge: function () {
    return this.age;
  },
};

extend(student, added);

student.getAge(52);
console.log(student.getAge());
```

얕은 복사를 사용하는 **[extend()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/extends)** 함수를 사용하여 student 객체를 확장시켰다.

### 2-2. 클래스 기반의 상속

```javascript
function Person(arg) {
  this.name = arg;
}

Person.prototype.setName = function (value) {
  this.name = value;
};

Person.prototype.getName = function () {
  return this.name;
};

function Student(arg) {}

var you = new Person("white");
Student.prototype = you;

var me = new Student("jesse");
me.setName("jesse");
console.log(me.getName());
```

1. Student 함수 객체의 프로토타입으로 하여금 Person 함수 객체의 인스턴스를 참조하게 만들었다.
2. Student 함수 객체로 생성된 객체 me의 [[Prototype]] 링크가 생성자의 프로토타입 프로퍼티 student.prototype인 you를 가리킨다.
3. new Person()으로 만들어진 객체의 [[Prototype]] 링크는 Person.prototype을 가리키는 프로토타입 체인이 형성된다.
4. 객체 me는 Person.prorotype 프로퍼티에 접근할 수 있고, setName()과 getName()을 호출할 수 있다.

```javascript
var me = new Student("jesse");
```

me 인스턴스를 생성할 때 부모 클래스인 Person의 생성자를 호출하지 않았다. 결국 생성된 me 객체는 빈 객체이다. 이렇게 부모의 생성자가 호출되지 않으면, 인스턴스의 초기화가 제대로 이루어지지 않아 문제가 발생할 수 있다.

```javascript
function Student(arg) {
  Person.apply(this, arguments);
}
```

Student 함수 안에서 새롭게 생성된 객체를 apply 함수의 첫 번째 인자로 넘겨 Person 함수를 실행시킨다. 클래스 간의 상속에서 하위 클래스의 인스턴스를 생성할 때, 부모 클래스의 생성자를 호출해야 하는데, 이 경우에 필요한 방식이다. 현재는 자식 클래스의 객체가 부모 클래스의 객체를 프로토타입 체인으로 직접 접근하지만 각각의 인스턴스는 독립적일 필요가 있다.

```javascript
function Person(arg) {
  this.name = arg;
}

Function.prototype.method = function (name, func) {
  this.prototype[name] = func;
};

Person.method("setName", function (value) {
  this.name = value;
});
Person.method("getName", function () {
  return this.name;
});

function Student(arg) {}

function F() {}
F.prototype = Person.prototype;
Student.prototype = new F();
Student.prototype.constructor = Student;
Student.super = Person.prototype;

var me = new Student();
me.setName("white");
console.log(me.getName());
```

빈 함수 F()를 생성하고, F()의 인스턴스를 Person.prototype과 Student 사이에 두어 서로 독립적으로 만들었다. Person 함수 객체에서 this에 바인딩되는 것은 Student의 인스턴스가 접근할 수 없다.

```javascript
var inherit = (function (Parent, Child) {
  var F = function () {};
  return function (Parent, Child) {
    F.prototype = Parent.prototype;
    Child.prototype = new F();
    Child.prototype.constructor = Child;
    Child.super = Parent.prototype;
  };
})();
```

클로저는 F() 함수를 지속적으로 참조하므로, F()는 가비지 컬렉션의 대상이 되지 않고 계속 남아있다. 이를 이용해 함수 F()의 생성은 단 한 번 이루어지고 inherit 함수가 계속해서 호출되어도 함수 F()의 생성을 새로 할 필요가 없다.

## 3. 캡슐화

- 캡슐화란 기본적으로 관련된 여러 가지 정보를 하나의 틀 안에 담는 것을 의미한다.
- 정보 은닉의 개념이 이 부분을 담당한다.

```javascript
var Person = function (arg) {
  var name = arg ? arg : "white";
  this.getName = function () {
    return name;
  };
  this.setName = function (arg) {
    name = arg;
  };
};

var me = new Person();
console.log(me.getName());
me.setName("jesse");
console.log(me.getName());
console.log(me.name); // undefined
```

1. private 멤버로 name을 선언하고, public 메서드로 getName()과 setName()을 선언하였다.
2. this 객체의 프로퍼티로 선언하면 외부에서 new 키워드로 생성한 객체로 접근할 수 있지만, var로 선언된 멤버들은 외부에서 접근이 불가능하다.
3. public 메서드가 클로저 역할을 하면서 private 멤버인 name에 접근할 수 있다.

이것이 자바스크립트에서 할 수 있는 기본적인 정보 은닉 방법이다.

```javascript
// 좀 더 깔끔하게
var Person = function (arg) {
  var name = arg ? arg : "white";

  return {
    getName: function () {
      return name;
    },
    setName: function () {
      name = arg;
    },
  };
};

var me = Person();
// var me = new Person();
console.log(me.getName());
```

1. Person 함수를 호출하여 객체를 반환받는다. 이 객체에 Person 함수의 private 멤버에 접근할 수 있는 메서드들이 담겨있다.
2. 사용자는 반환받는 객체로 메서드를 호출할 수 있고, private 멤버에 접근할 수 있다.
3. 접근하는 private 멤버가 객체나 배열이면 얕은 복사로 참조만을 반환하므로 사용자가 이후 이를 쉽게 변경할 수 있으니 주의해야 한다.

```javascript
var ArrCreate = function (arg) {
  var arr = [1, 2, 3];

  return {
    getArr: function () {
      return arr;
    },
  };
};

var obj = ArrCreate();
// var me = new Person();
var arr = obj.getArr();
arr.push(5);
console.log(obj.getArr()); // [ 1,2,3,5 ]
```

이와 같은 문제가 있으므로 프로그래머는 객체를 반환하는 경우 신중해야 한다. 보통의 경우, 객체를 반환하지 않고 객체의 주요 정보를 새로운 객체에 담아서 반환하는 방법을 많이 사용한다. 꼭 객체가 반환되어야 하는 경우에는 깊은 복사로 복사본을 만들어서 반환하는 방법을 사용하는 것이 좋다.

```javascript
var Person = (function (arg) {
  var name = arg ? arg : "white";

  var Func = function () {};
  Func.prototype = {
    getName: function () {
      return name;
    },
    setName: function () {
      name = arg;
    },
  };

  return Func;
})();

var me = new Person();
console.log(me.getName());
```

클로저를 활용하여 name에 접근할 수 없게 했다. 즉시 실행 함수에서 반환되는 Func이 클로저가 되고 이 함수가 참조하는 name 프로퍼티가 자유 변수가 된다. 따라서 사용자는 name에 대한 접근이 불가능하다.
