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

1. **[bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)** 함수는 커링 기법을 활용한 함수이다.
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

### 3-4. 래퍼

- 래퍼란 특정 함수를 자신의 함수로 덮어쓰는 것을 말한다.
- 사용잔느 원래 함수 기능을 잃어버리지 않은 상태로 자신의로직을 수행할 수 있어야 한다.

```javascript
function wrap(object, method, wrapper) {
  var fn = object[method];
  return (object[method] = function () {
    return wrapper.apply(
      this,
      [fn].concat(Array.prototype.slice.call(arguments))
    );
    // return wrapper.apply(
    //   this,
    //   [fn.bind(this)].concat(Array.prototype.slice.call(arguments))
    // );
  });
}

Function.prototype.original = function (value) {
  this.value = value;
  console.log("value : " + this.value);
};

var mywrap = wrap(Function.prototype, "original", function (orig_func, value) {
  this.value = 20;
  orig_func(value);
  console.log("wrapper value : " + this.value);
});

var obj = new mywrap("saul");
// value : saul
// wrapper value : 20
```

1. Function.prototype의 original 함수는 인자로 넘어온 값을 value에 할당하고 출력하는 기능을 한다.
2. 세 번째 인자로 넘긴 자신의 익명 함수를 Function.prototype.original에 덮어쓰기 위해 wrap 함수를 호출하였다.
3. 사용자는 자신의 익명 함수의 첫 번째 인자로 원래 함수의 참조를 받을 수 있다.
4. 주석된 bind 함수를 이용하면 original()이 호출될 때의 this와 반환되는 익명 함수의 this가 다른 점을 해결할 수 있다.

래퍼는 기존에 제공되는 함수에서 사용자가 원하는 로직을 추가하고 싶다거나, 기존의 버그를 피해가고자 할 때 많이 사용된다.  
특히, 특정 플랫폼에서 버그를 발생시키는 함수가 있을 경우 이를 컨트롤하는 데 용이하다.

### 3-5. 반복 함수

#### 3-5-1. each

- **[each()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)** 함수는 배열의 각 요소 혹은 객체의 각 프로퍼티를 하나씩 꺼내서 차례대로 특정 함수에 인자로 넣어 실행시키는 역할을 한다.

```javascript
function each(obj, fn, args) {
  if (obj.length === undefined)
    for (var i in obj) fn.apply(obj[i], args || [i, obj[i]]);
  else
    for (var i = 0; i < obj.length; i++) fn.apply(obj[i], args || [i, obj[i]]);
  return obj;
}

each([1, 2, 3], function (idx, num) {
  console.log(idx + ": " + num);
});

var saul = {
  name: "saul",
  age: 30,
  sex: "Male",
};

each(saul, function (idx, value) {
  console.log(idx + ": " + value);
});
```

1. obj에 length가 있는 경우와 없는 경우로 나누어서, 루프를 돌며 각 요소를 인자로 하여 차례대로 함수를 호출한다.
2. each() 함수에서 사용자 함수를 호출할 때 넘기는 인자의 순서나 구성이 라이브러리에 따라 다를 수 있다.

#### 3-5-2. map

- **[map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)** 함수는 배열의 각 요소를 꺼내서 사용자 정의 함수를 적용시켜 새로운 값을 얻은 후, 새로운 배열에 넣는다.

```javascript
Array.prototype.map = function (callback) {
  // this가 null인지, 배열인지 체크
  // callback이 함수인지 체크

  var obj = this;
  var value, mapped_value;
  var A = new Array(obj.length);

  for (var i = 0; i < obj.length; i++) {
    value = obj[i];
    mapped_value = callback.call(null, value);
    A[i] = mapped_value;
  }

  return A;
};

var arr = [1, 2, 3];
var new_arr = arr.map(function (value) {
  return value * value;
});

console.log(new_arr); // [ 1, 4, 9 ]
```

사용자는 map() 함수를 이용하여 각 요소의 제곱값을 반환하는 순수 함수를 넣어 실행시킨 뒤 새로운 배열을 반환 받을 수 있다.

#### 3-5-3. reduce

- **[reduce()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)**는 배열의 각 요소를 하나씩 꺼내서 사용자의 함수를 적용시킨 뒤, 그 값을 계속해서 누적시키는 함수이다.

```javascript
Array.prototype.reduce = function (callback, memo) {
  // this가 null인지, 배열인지 체크
  // callback이 함수인지 체크

  var obj = this;
  var value,
    accumulated_value = 0;

  for (var i = 0; i < obj.length; i++) {
    value = obj[i];
    accumulated_value = callback.call(null, accumulated_value, value);
  }

  return accumulated_value;
};

var arr = [1, 2, 3];
var accumulated_val = arr.reduce(function (a, b) {
  return a + b * b;
});

console.log(accumulated_val); // 14
```

각 요소를 사용자가 원하는 특정 연산으로 누적된 값을 반환받고자 할 때 유용하게 사용된다.
