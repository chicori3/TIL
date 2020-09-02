## 4. 객체지향 프로그래밍 응용 예제

### 4-1. 클래스의 기능을 가진 subClass 함수

앞서 공부한 다음 세 가지를 활용해서 구현한다.

- 함수의 프로토타입 체인
- extend 함수
- 인스턴스를 생성할 때 생성자 호출

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

> hasOwnProperty 메서드

    Object.prototype 프로퍼티에 정의되어 있는 메서드로서, 인자로 넘기는 이름에 해당하는 프로퍼티가 객체 내에 있는지를 판단한다.
    여기서 프로퍼티를 찾을 때, 다음 예제와 같이 프로토타입 체인을 타고 올라가지 않고 해당 객체 내에서만 찾는다는 것에 유의한다.

    ```javascript
    o = new Object();
    o.prop='exists';
    o.hasOwnProperty('prop'); // returns true
    o.hasOwnProperty('toString'); // returns false
    o.hasOwnProperty('hasOwnProperty'); // returns false
    ```
