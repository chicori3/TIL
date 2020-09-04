## 3. 자바스크립트에서의 함수형 프로그래밍을 활용한 주요 함수

### 3-1. 함수 적용

- 함수 적용은 함수형 프로그래밍에서 사용되는 용어다.
- 함수형 프로그래밍에서는 특정 데이터를 여러 가지 함수를 적용시키는 방식으로 작업을 수행한다
- 단순히 입력을 넣고 출력을 받는 기능이 아니라, 인자 혹은 반환 값으로 전달된 함수를 특정 데이터에 적용시키는 개념이다.

### 3-2. 커링

- 커링이란 특정 함수에서 정의된 인자의 일부를 넣어 고정시키고, 나머지를 인자로 받는 새로운 함수를 만드는 것을 의미한다.

```javascript
function calculate(a, b, c) {
  return a * b + c;
}

function curry(func) {
  var args = Array.prototype.slice.call(arguments, 1);

  return function () {
    return func.apply(null, args.concat(Array.prototype.slice.call(arguments)));
  };
}

var new_func1 = curry(caclulate, 1);
console.log(new_func1(2, 3)); // 5 // 1*2+3=5
var new_func2 = curry(calculate, 1, 3);
console.log(new_func2(3)); // 6 // 1*3+3=6
```

1. calculate() 함수는 인자 세 개를 받아 연산을 수행하고 결과값을 반환한다.
2. curry() 함수로 각각 인자를 가진 새로운 함수 new_func를 만들었다.
3. curry() 함수로 넘어온 인자를 args에 담아 놓고, 새로운 함수 호출로 넘어온 인자와 합쳐서 함수를 적용한다.
4. 자바스크립트에서 커링을 기본적으로 제공하지 않지만 Function.prototype에 정의하여 사용할 수 있다.

```javascript
// 커링 함수 정의
Function.prototype.curry = function () {
  var fn = this,
    args = Array.prototype.slice.call(arguments);
  return function () {
    return fn.apply(this, args.concat(Array.prototype.slice.call(arguments)));
  };
};
```

```javascript
// 첫 번째, 세 번째 인자 고정
function calculate(a, b, c) {
  return a * b + c;
}

function curry2(func) {
  var args = Array.prototype.slice.call(arguments, 1);

  return function () {
    var arg_idx = 0;
    for (var i = 0; i < args.length && arg_idx < arguments.length; i++) {
      if (args[i] === undefined) {
        args[i] = arguments[arg_idx++];
      }
    }
    return func.apply(null, args);
  };
}

var new_func = curry2(calculate, 1, undefined, 4);
console.log(new_func(3)); // 7 // 1*3+4=7
```

1. curry2() 함수를 사용할 때 주의할 점은 curry2를 호출할 때 calcultate() 함수가 원하는 인자를 전부 넣어야 한다는 것이다.
2. 그 중 고정시키지 않을 인자를 undefined로 넘기면 된다.
3. curry2()를 호출할 때 넘어온 인자로 루프를 돌면서 undefined인 요소를 새로운 함수를 호출할 때 넘어온 인자로 대체한다.
4. 이와 같이 함수를 부분적으로 적용하여 새로운 함수를 반환받는 방식을 함수의 부분 적용이라고 한다.

### 3-3. bind

```javascript
Function.prototype.bind = function (thisArg) {
  var fn = this,
    slice = Array.prototype.slice,
    args = slice.call(arguments, 1);
  return function () {
    return fn.apply(thisArg, args.concat(slice.call(arguments)));
  };
};
```

1. [bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) 함수는 커링 기법을 활용한 함수이다.
2. 사용자가 고정시키고자 하는 인자를 bind() 함수를 호출할 때 넘겨주고 반환받은 함수를 호출하면서 나머지 가변 인자를 넣어줄 수 있다.
3. Curry() 함수와 다른 점은 함수를 호출할 때 this에 바인딩시킬 객체를 사용자가 넣어줄 수 있다는 점이다.

```javascript
var print_all = function (arg) {
  for (var i in this) console.log(i + " : " + this[i]);
  for (var i in arguments) console.log(i + " : " + arguments[i]);
};

var myobj = { name: "saul" };

var myfunc = print_all.bind(myobj);
myfunc(); // "name : saul"

var myfunc1 = print_all.bind(myobj, "white", "mike");
myfunc1("jesse");
// " name : saul " " 0 : white " " 1 : mike " " 2 : jesse "
```

1. myfunc() 함수는 myobj 객체를 this에 바인딩시켜 print_all() 함수를 실행하는 새로운 함수이다.
2. my-func1() 함수를 실행하면 인자도 bind() 함수에 모두 넘겨진다.
3. 특정 함수에 원하는 객체를 바인딩시켜 새로운 함수를 사용할 때 bind() 함수가 사용된다.
