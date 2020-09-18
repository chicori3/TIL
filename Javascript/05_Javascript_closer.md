## 4. 클로저

### 4-1. 클로저의 개념

```javascript
function outerFunc() {
  var x = 10;
  var innerFunc = function () {
    console.log(x);
    return innerFunc;
  };
}

var inner = outerFunc();
inner(); // 10
```

자바스크립트의 함수는 일급 객체로 취급된다. 이는 함수를 다른 함수의 인자로 넘길 수도 있고, return으로 함수를 통째로 반환받을 수도 있음을 의미한다. 여기서 최종 반환되는 함수가 외부 함수의 지역변수에 접근하고 있다는 것이 중요하다. 이 지역변수에 접근하려면, 함수가 종료되어 외부 함수의 컨텍스트가 반환되더라도 변수 객체는 반환되는 내부 함수의 스코프 체인에 그대로 남아있어야만 접근할 수 있다. **이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 함수를 클로저라고 한다.** 예제에서는 outerFunc에서 선언된 x를 참조하는 innerFunc가 클로저가 된다. 그리고 클로저로 참조되는 외부 변수 즉, outerFunc의 x와 같은 변수를 **자유 변수**라고 한다.

```javascript
function outerFunc(arg1, arg2) {
  var local = 8;
  function innerFunc(innerArg) {
    console.log((arg1 + arg2) / (innerArg + local));
  }
  return innerFunc;
}
var exam1 = outerFunc(2, 4);
exam1(2);
```

1. outerFunc()가 실행되면서 생성되는 변수 객체가 스코프 체인에 들어가고, 이 스코프 체인은 innerFunc의 스코프 체인으로 참조된다.
2. outerFunc() 함수가 종료되었지만, 내부 함수 innerFunc()의 [[scope]]로 참조되므로 접근이 가능하다.
3. 이후에 exam1(n)을 호출하여도, innerFunc()에서 참조하고자 하는 변수 local에 접근할 수 있다.

> innerFunc()에서 접근하는 변수 대부분이 스코프 체인의 첫 번째 객체가 아닌 그 이후의 객체에 존재한다. 대부분의 클로저에서는 스코프 체인에서 뒤쪽에 있는 객체에 자주 접근하므로, 성능을 저하시키는 이유로 지목되기도 한다.

### 4-2. 클로저의 활용

클로저는 성능적인 면과 자원적인 면에서 약간 손해를 볼 수 있으므로 무차별적으로 사용해서는 안 된다.

#### 4-2-1. 특정 함수에 사용자가 정의한 객체의 메서드 연결하기

```javascript
function HelloFunc() {
  this.greeting = "hello";
}

HelloFunc.prototype.call = function (func) {
  func ? func(this.greeting) : this.func(this.greeting);
};

var userFunc = function (greeting) {
  console.log(greeting);
};

var objHello = new HelloFunc();
objHello.func = userFunc;
objHello.call(); // hello
```

1. 함수 HelloFunc는 greeting 변수가 있고, func 프로퍼티로 참조되는 함수를 call() 함수로 호출한다.
2. HelloFunc.prototype.call()을 보면 자신의 지역 변수인 greeting만을 인자로 사용자가 정의한 함수에 넘긴다.
3. userFunc() 함수를 정의하여 objHello.func()에 참조시킨 뒤, HelloFunc()의 지역 변수인 greeting을 화면에 출력시킨다.

```javascript
function saySomething(obj, methodName, name) {
  return function (greeting) {
    return obj[methodName](greeting, name);
  };
}

function newObj(obj, name) {
  obj.func = saySomething(this, "who", name);
  return obj;
}

newObj.prototype.who = function (greeting, name) {
  console.log(greeting + " " + (name || "everyone"));
};

var obj1 = new newObj(objHello, "zzoon");
obj1.call(); // hello zzoon
```

1. 첫 번째로 인자로 받는 obj는 HelloFunc()의 객체가 되고, 두 번째 인자는 사용자가 출력을 원하는 이름이 된다.
2. 첫 번째 인자 obj의 func 프로퍼티에 saySomething() 함수에서 반환되는 함수를 참조하고 반환한다. obj1은 인자로 넘겼던 objHello 객체에서 func 프로퍼티에 참조된 함수만 바뀐 객체가 된다.
3. 반환되는 함수가 HelloFunc이 원하는 function(greeting){} 형식의 함수가 되는데, 이것이 HelloFunc 객체의 func로 참조된다.
4. obj1.call()로 실행되는 것은 실질적으로 newObj.prototype.who()가 된다.

이와 같은 방식으로 사용자는 자신의 객체 메서드인 who 함수를 HelloFunc에 연결시킬 수 있다. 여기서 클로저는 saySomething()에서 반환되는 function(greeting){}이 되고, 이 클로저는 자유 변수 obj, methodName, name을 참조한다.

#### 4-2-2. 함수의 캡슐화

다음과 같은 함수를 작성한다고 가정해보자.

> "I am XXX. I live in XXX. I'am XX years old."라는 문장을 출력하는데, XX 부분은 사용자에게 인자로 입력 받아 값을 출력하는 함수.

가장 먼저 생각할 수 있는 것은 앞 문장 템플릿을 전역 변수에 저장하고, 사용자의 입력을 받은 후, 전역 변수에 접근하여 완성된 문장을 출력하는 방식으로 함수를 작성하는 것이다.

```javascript
var getCompletedStr = function () {
  var buffAr = ["I am ", "", ". I live in ", "", ". I'am ", "", " years old."];

  return function (name, city, age) {
    buffAr[1] = name;
    buffAr[3] = city;
    buffAr[5] = age;

    return buffAr.join("");
  };
};

var str = getCompletedStr("zzoon", "seoul", 16);
console.log(str);
```

예제에서 주의해서 봐야 할 점은 변수 getCompletedStr에 익명의 함수를 즉시 실행시켜 반환되는 함수를 할당하는 것이다. 이 반환되는 함수가 클로저가 되고, 이 클로저는 자유 변수 buffAr을 스코프 체인에서 참조할 수 있다.

#### 4-2-3. setTimeout()에 지정되는 함수의 사용자 정의

[setTimeout()](https://developer.mozilla.org/ko/docs/Web/API/WindowTimers/setTimeout) 함수는 브라우저에서 제공하는 함수인데, 첫 번째 인자로 넘겨지는 함수 실행의 스케쥴링을 할 수 있다. 두 번째 인자인 밀리 초 단위 숫자만큼의 시간 간격으로 해당 함수를 호출한다.
setTimeout()으로 자신의 코드를 호출하고 싶다면 첫 번째 인자로 해당 함수 객체의 참조를 넘겨주면 되지만, 이것으로는 실제 실행될 때 함수에 인자를 줄 수 없는 데 클로저로 해결할 수 있다.

```javascript
function callLater(obj, a, b) {
  return function () {
    obj["sum"] = a + b;
    console.log(obj["sum"]);
  };
}

var sumObj = {
  sum: 0,
};

var func = callLater(sumObj, 1, 2);
setTimeout(func, 500);
```

callLater를 setTimeout 함수로 호출하려면, 변수 func에 함수를 반환받아 setTimeout() 함수의 첫 번째 인자로 넣어주면 된다. 반환받는 함수는 당연히 클로저고, 사용자가 원하는 인자에 접근할 수 있다.

### 4-3. 클로저를 활용할 때 주의사항

클로저는 자바스크립트의 강력한 기능이지만, 너무 남발하여 사용하면 안 된다.

#### 4-3-1. 클로저의 프로퍼티값이 쓰기 가능하므로 그 값이 여러번 호출로 항상 변할 수 있다

```javascript
function outerFunc(argNum) {
  var num = argNum;
  return function (x) {
    num += x;
    console.log("num: " + num);
  };
}
var exam = outerFunc(40);
exam(5);
exam(-10);
```

> exam 값을 호출할 때마다, 자유 변수 num의 값은 계속해서 변화한다.

#### 4-3-3. 루프 안에서 클로저를 활용할 때는 주의하자

```javascript
function countSeconds(howMany) {
  for (var i = 1; i <= howMany; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }
}
countSeconds(3);
```

예제는 1, 2, 3을 1초 간격으로 출력하려는 의도지만 결과는 4가 연속 3번 1초 간격으로 출력된다. setTimeout 함수의 인자로 들어가는 함수는 자유 변수 i를 참조한다. 이 함수가 실행되는 시점은 countSeconds() 함수의 실행이 종료된 이후이고, i 값은 이미 4가 된 상태이다. 그러므로 setTimeout()로 실행되는 함수는 4를 출력하게 된다.

```javascript
function countSeconds(howMany) {
  for (var i = 1; i <= howMany; i++) {
    (function (currentI) {
      setTimeout(function () {
        console.log(currentI);
      }, currentI * 1000);
    })(i);
  }
}
countSeconds(3);
```

즉시 실행 함수를 실행시켜 루프 i 값을 currentI에 복사해서 setTimeout()에 들어갈 함수에서 사용하면 원하는 결과를 얻을 수 있다.
