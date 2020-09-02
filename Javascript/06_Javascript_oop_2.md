## 4. 객체지향 프로그래밍 응용 예제

### 4-1. 클래스의 기능을 가진 subClass 함수

앞서 공부한 다음 세 가지를 활용해서 구현한다.

- 함수의 프로토타입 체인
- extend 함수
- 인스턴스를 생성할 때 생성자 호출 (여기서는 \_init 함수가 생성자를 뜻한다)

#### 4-1-1. subClass 함수 구조

subClass는 상속받을 클래스에 넣을 변수 및 메서드가 담긴 객체를 인자로 받아 부모 함수를 상속 받는 자식 클래스를 만든다.
여기서 부모 함수는 subClass() 함수를 호출할 때 this 객체를 의미한다.

```javascript
var SuperClass = subClass(obj);
var SubClass = SuperClass.subClass(obj);
```

이처럼 SuperClass를 상속받는 subClass를 만들고자 할 때, SuperClass.subClass()의 형식으로 호출하게 구현한다.
참고로 최상위 클래스인 SuperClass는 자바스크립트의 Function을 상속받게 한다.
함수 subClass의 구조는 다음과 같이 구성된다.

```javascript
function subClass(obj) {
  // 1. 자식 클래스 생성
  // 2. 생성자 호출
  // 3. 프로토타입 체인을 활용한 상속 구현
  // 4. obj를 통해 들어온 변수 및 메서드를 자식 클래스에 추가
  // 5. 자식 함수 객체 반환
}
```

#### 4-1-2. 자식 클래스 생성 및 상속

```javascript
function subClass(obj) {
......
  var parent = this;
  var F = function () {};

  var child = function () {};

  F.prototype = parent.prototype;
  child.prototype = new F();
  child.prototype.constructor = child;
  child.parent = parent.prototype;
  child.parent_constructor = parent;
......
  return child;
}
```

- 자식 클래스는 child라는 이름의 함수 객체를 생성함으로써 만들어졌다.
- 부모 클래스를 가리키는 parent는 this를 그대로 참조한다.

#### 4-1-3. 자식 클래스 확장

이제 사용자가 인자로 넣은 객체를 자식 클래스에 넣어 자식 클래스를 확장할 차례다.

```javascript
for (var i in obj) {
  if (obj.hasOwnProperty(i)) {
    child.prototype[i] = obj[i];
  }
}
```

- [extend()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/extends) 함수의 역할을 하는 코드를 넣었다.
- 간단히 얕은 복사로 객체의 프로퍼티를 복사하는 방식을 택했다.

> [hasOwnProperty](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty) 메서드

    Object.prototype 프로퍼티에 정의되어 있는 메서드로서, 인자로 넘기는 이름에 해당하는 프로퍼티가 객체 내에 있는지를 판단한다.
    여기서 프로퍼티를 찾을 때, 다음 예제와 같이 프로토타입 체인을 타고 올라가지 않고 해당 객체 내에서만 찾는다는 것에 유의한다.

```javascript
o = new Object();
o.prop = "exists";
o.hasOwnProperty("prop"); // returns true
o.hasOwnProperty("toString"); // returns false
o.hasOwnProperty("hasOwnProperty"); // returns false
```

#### 4-1-4. 생성자 호출

클래스의 인스턴스가 생성될 때, 클래스 내에 정의된 생성자가 호출돼야 한다.
물론 부모 클래스의 생성자 역시 호출되어야 한다.

```javascript
var child = function () {
  var parent = child.parent;
  if (parent._init) {
    parent._init.apply(this, arguments);
  }
  if (child.prototype._init) {
    child.prototype._init.apply(this, arguments);
  }
};
```

위 코드는 문제를 안고 있다.
parent.\_init이나 child.prototype.\_init을 찾을 때, \_init 프로퍼티가 없으면 프로토타입 체인으로 상위 클래스의 \_init 함수를 찾아서 호출할 수 있다. 따라서 앞에서 소개된 hasOwnProperty 함수를 활용하는 것이 좋다.

```javascript
var child = function () {
  var parent = child.parent;
  if (parent.hasOwnProperty("_init")) {
    parent._init.apply(this, arguments);
  }
  if (child.prototype.hasOwnProperty("_init")) {
    child.prototype._init.apply(this, arguments);
  }
};
```

앞 코드는 단순히 부모와 자식이 한 쌍을 이루었을 때만 제대로 작동한다.
자식을 또 다른 함수가 다시 상속받았을 때는 문제가 생긴다.

```javascript
var SuperClass = subClass();
var SubClass = SuperClass.subClass();
var Sub_SubClass = SubClass.subClass();

var instance = new Sub_SubClass();
```

이 코드에서 instance를 생성할 때, SuperClass의 생성자가 호출되지 않는다.
따라서 부모 클래스의 생성자를 호출하는 코드는 재귀적으로 구현할 필요가 있다.

```javascript
var child = function () {
  var _parent = child.parent_constructor;

  if (_parent && _parent !== Function) {
    // 현재 클래스의 부모 생성자가 있으면 그 함수를 호출한다. 부모가 Function일 경우에는 최상위 클래스이므로 호출하지 않는다.
    _parent.apply(this, arguments); // 부모 함수의 재귀적 호출
  }

  if (child.prototype.hasOwnProperty("_init")) {
    child.prototype._init.apply(this, arguments);
  }
};
```

#### 4-1-5. subClass 보완

parent를 단순히 this.prototype으로 지정해서는 안 된다.
처음에 최상위 클래스를 Function을 상속받는 것으로 정했는데, 현재 코드에는 이를 처리하는 코드가 없다.

```javascript
parent = this;
```

```javascript
var parent = this === window ? Function : this; // Node.js의 경우에는 global을 사용한다.
```

subClass 안에서 생성하는 자식 클래스의 역할을 하는 함수는 subClass 함수가 있어야 한다.

```javascript
child.subClass = arguments.callee;
```

[arguments.callee](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments/callee)는 현재 호출된 함수를 의미하는데, 현재 호출된 함수가 subClass이므로 child.subClass는 subClass 함수를 참조한다.

```javascript
// subClass 함수의 전체 코드
function subClass(obj) {
  var parent = this === window ? Function : this;
  var F = function () {};

  var child = function () {
    var _parent = child.parent;

    if (_parent && _parent !== Function) {
      _parent.apply(this, arguments);
    }

    if (child.prototype._init) {
      child.prototype._init.apply(this, arguments);
    }
  };

  F.prototype = parent.prototype;
  child.prototype = new F();
  child.prototype.constructor = child;
  child.parent = parent;
  child.subClass = arguments.callee;

  for (var i in obj) {
    if (obj.hasOwnProperty(i)) {
      child.prototype[i] = obj[i];
    }
  }

  return child;
}
```

#### 4-1-6. subClass 활용

```javascript
var person_obj = {
  _init: function () {
    console.log("person init");
  },
  getName: function () {
    return this._name;
  },
  setName: function (name) {
    this._name = name;
  },
};

var student_obj = {
  _init: function () {
    console.log("student init");
  },
  getName: function () {
    return "Student Name: " + this._name;
  },
};

var Person = subClass(person_obj); // Person 클래스 정의
var person = new Person(); // person init 출력
person.setName("white");
console.log(person.getName()); // white

var student = Person.subClass(student_obj); // Student 클래스 정의
var student = new Student(); // person init, student init 출력
student.setName("jesse"); //
console.log(sutdent.getName()); // Student Name : jesse

console.log(Person.toString()); // Person이 Function을 상속받는지 확인
```

#### 4-1-7. subClass 함수에 클로저 활용

```javascript
var F = function () {};
```

이 함수 객체는 subClass 함수가 호출될 때마다 생성된다. 클로저로 단 한번만 생성되게 수정해보자.

```javascript
var subClass = function () {
  var F = function () {};

  var subClass = function(obj){
      ......
  }

  return subClass;
}();
```

즉시 실행 함수로 새로운 컨텍스트를 만들어서 F() 함수 객체를 생성하였다. 그리고 이 F() 함수 객체를 참조하는 안쪽의 subClass() 함수를 반환받는다. 이렇게 하면 F() 함수 객체는 클로저에 엮여서 가비지 컬렉션의 대상이 되지 않고, subClass() 함수를 호출할 때마다 사용된다.

### 4-2. subClass 함수와 모듈 패턴을 이용한 객체지향 프로그래밍

캡슐화의 중요한 개념인 정보를 은닉하려면 모듈 패턴은 상당히 유용하다.

```javascript
var person = function (arg) {
  var name = undefined;

  return {
    _init: function (arg) {
      name = arg ? arg : "white";
    },
    getName: function () {
      return name;
    },
    setName: function (arg) {
      name = arg;
    },
  };
};

Person = subClass(person());
var jesse = new Person("jesse");
console.log(jesse.getName());

Student = Person.subClass();
var student = new Student("student");
console.log(student.getName());
```

1. person 함수 객체는 name의 정보를 캡슐화시킨 객체를 반환받는 역할을 한다.
2. 반환받은 객체는 subClass() 함수의 인자로 들어가 클래스의 역할을 하는 Person 함수 객체를 완성시킬 수 있다.
3. Person 함수 객체를 활용하여 상속을 구현할 수 있다.
