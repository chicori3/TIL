# 6. 객체지향 프로그래밍

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
