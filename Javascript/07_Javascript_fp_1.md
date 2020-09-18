# 07. 함수형 프로그래밍

함수형 프로그래밍은 프로그래밍의 여러 가지 패러다임 중 하나이다.

## 1 함수형 프로그래밍의 개념

- 함수형 프로그래밍은 함수의 조합으로 작업을 수행함을 의미한다.
- 작업이 이루어지는 동안 작업에 필요한 데이터와 상태는 변하지 않는다.
- 오직 변할 수 있는 것은 함수뿐이며 함수가 연산의 대상이 된다.

**함수형 프로그래밍을 표현하는 슈도 코드**

```javascript
f1 = encrypt1;
f2 = encrypt2;
f3 = encrypt3;
```

1. f1, f2, f3은 입력값이 정해지지 않고, 서로 다흔 암호화 알고리즘만 있다.

```javascript
pure_value = "saul";
encrypted_value = get_encrypted(x);
```

2. pure_value는 암호화할 문자열이고, encrypted_value는 암호화된 문자열이다.
3. get_encrypted()는 암호화 함수를 받아서 입력받은 함수로 pure_value를 암호화한 후 반환한다.

```javascript
encrypted_value = get_encrypted(f1);
encrypted_value = get_encrypted(f2);
encrypted_value = get_encrypted(f3);
```

4. pure_value는 작업에 필요한 데이터고 작업이 수행되는 동안 변하지 않는다.
5. get_encrypted()가 작업하는 동안 변할 수 있는 것은 입력으로 들어오는 함수뿐이다.
6. f1, f2, f3는 외부에 아무런 영향을 미치지 않는 함수(**순수 함수**)라고 한다.
7. get_encrypted 함수의 결과값은 encrypted_value라는 값이지만 결과값을 또 다른 형태의 함수로서 반환할 수 있는데, 함수를 또 하나의 값으로 간주하여 함수의 인자 혹은 반환값으로 사용할 수 있는 함수를 **고계 함수**라고 한다.

내부 데이터 및 상태는 그대로 둔 채 제어할 함수를 변경 및 조합함으로써 원하는 결과를 얻어내는 것이 함수형 프로그래밍의 중요한 특성이다.
높은 수준의 모듈화가 가능한 장점이 있다. 순수 함수의 조건을 충족하는 함수 구현으로 모듈 집약적인 프로그래밍이 가능하다.

> 함수형 프로그래밍의 반대되는 개념을 명령형 프로그래밍이라고 한다.

## 2. 자바스크립트에서의 함수형 프로그래밍

자바스크립트에서도 함수형 프로그래밍이 가능하다.

- 일급 객체로서의 함수
- 클로저

두 가지 기능을 지원하기 때문이다.

```javascript
var f1 = function (input) {
  var result;
  // 암호화 작업 수행
  result = 1;
  return result;
};

var f2 = function (input) {
  var result;
  // 암호화 작업 수행
  result = 2;
  return result;
};

var f3 = function (input) {
  var result;
  // 암호화 작업 수행
  result = 3;
  return result;
};

var get_encrypted = function (func) {
  var str = "saul";

  return function () {
    return func.call(null, str);
  };
};

var encrypted_value = get_encrypted(f1)();
console.log(encypted_value);
var encrypted_value = get_encrypted(f1)();
console.log(encypted_value);
var encrypted_value = get_encrypted(f1)();
console.log(encypted_value);
```

이처럼 자바스크립트에서 함수형 프로그래밍 슈도를 구현할 수 있다. 이것이 가능한 이유는 함수가 일급 객체로 취급되기 때문이다. 그래서 함수의 인자로 함수를 넘기고, 결과로 함수를 반환할 수도 있다. 게다가 변수 str 값이 영향을 받지 않게 하려고 클로저를 사용했다. 위 예제에서 get_encrypted() 함수에서 반환하는 익명 함수가 클로저이다. 클로저에서 접근하는 변수 str은 외부에서는 접근할 수 없으므로 클로저로 함수형 프로그래밍의 개념을 정확히 구현해낼 수 있다.

### 2-1. 배열의 각 원소 총합 구하기

```javascript
// 배열의 각 원소 더한 값 구하기
function sum(arr) {
  var len = arr.length;
  var i = 0,
    sum = 0;

  for (; i < len; i++) {
    sum += arr[i];
  }

  return sum;
}

var arr = [1, 2, 3, 4];
console.log(sum(arr)); // 10
```

```javascript
// 배열의 각 원소 곱한 값 구하기
function multiply(arr) {
  var len = arr.length;
  var i = 0,
    result = 1;

  for (; i < len; i++) {
    result *= arr[i];
  }

  return result;
}

var arr = [1, 2, 3, 4];
console.log(multiply(arr)); // 24
```

두 예제는 명령형 프로그래밍 방식으로 작성된 코드이다. 배열의 각 원소를 다른 방식으로 산술한 결과값을 얻으려면 새로운 함수를 다시 구현해야 한다. 함수형 프로그래밍을 이용하면 이러한 수고를 덜 수 있다.

```javascript
function reduce(func, arr, memo) {
  var len = arr.length;
  i = 0;
  accum = memo;

  for (; i < len; i++) {
    accum = func(accum, arr[i]);
  }

  return accum;
}
```

[reduce()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 함수는 함수와 배열을 인자로 넘겨받고 루프를 돌면서 함수를 실행시킨다. 함수를 실행시켜 얻은 결과값은 변수 accum에 계속해서 저장한다. 루프가 끝나고 최종적으로 accum 값을 반환한다. 사용자는 reduce() 함수의 인자로 들어가는 함수를 직접 정의할 수 있다.

```javascript
var arr = [1, 2, 3, 4];

var sum = function (x, y) {
  return x + y;
};

var multiply = function (x, y) {
  return x * y;
};

console.log(reduce(sum, arr, 0));
console.log(reduce(multiply, arr, 1));
```

함수형 프로그래밍을 이용하여 코드를 훨씬 간결하게 작성할 수 있다. 또한, 다른 문제가 나오더라도 reduce() 함수로 결과를 얻을 수도 있다.

### 2-2. 팩토리얼

```javascript
// 명령형 프로그래밍 방식
function fact(num) {
  var val = 1;
  for (var i = 2; i <= num; i++) {
    val = val * i;
  }

  return val;
}

console.log(fact(100));
```

```javascript
// 재귀 호출 이용
function fact(num) {
  if (num === 0) return 1;
  else return num * fact(num - 1);
}

console.log(fact(100));
```

두 예제는 팩토리얼을 구현하는 데 성공했지만, 이런 종류의 함수 구현은 성능을 고려하게 된다.
앞서 연산한 결과를 캐시에 저장하여 사용할 수 있는 함수를 작성한다면 성능 향상에 도움이 된다.

```javascript
var fact = (function () {
  var cache = { 0: 1 };
  var func = function (n) {
    var result = 0;

    if (typeof cache[n] === "number") {
      result = cache[n];
    } else {
      result = cache[n] = n * func(n - 1);
    }

    return result;
  };

  return func();
})();

console.log(fact(10));
console.log(fact(20));
```

1. fact는 cache에 접근할 수 있는 클로저를 반환받는다.
2. 클로저로 숨겨지는 cache에는 팩토리얼을 연산한 값을 저장하고 있다.
3. 연산을 수행하는 과정에서 캐시에 저장된 값이 있으면 곧바로 그 값을 반환하는 방식이다.

### 2-3. 피보나치 수열

```javascript
var fibo = (function () {
  var cache = { 0: 0, 1: 1 };

  var func = function (n) {
    if (typeof cache[n] === "number") {
      result = cache[n];
    } else {
      result = cache[n] = func(n - 1) + func(n - 2);
    }

    return result;
  };

  return func;
})();

console.log(fibo(10));
```

클로저를 이용하여 cache를 캐시로 활용한다는 것이 같지만, cache의 초기값과 함수를 재귀 호출할 때 산술식이 다르다.

```javascript
var cacher = function (cache, func) {
  var calculate = function (n) {
    if (typeof cache[n] === "number") {
      result = cache[n];
    } else {
      result = cache[n] = func(calculate, n);
    }

    return result;
  };

  return calculate;
};
```

cacher 함수는 사용자 정의 함수와 초기 cache 값을 받아 연산을 수행한다. 사용자는 이 함수의 인자로 피보나치 수열이나 팩토리얼을 연산하는 함수를 정의하여 사용할 수 있다.

```javascript
var fact = cacher({ 0: 1 }, function (func, n) {
  return n * func(n - 1);
});

var fibo = cacher({ 0: 0, 1: 1 }, function (func, n) {
  return func(n - 1) + func(n - 2);
});

console.log(fact(10));
console.log(fibo(10));
```

함수형 프로그래밍이 수학에서 출발한 문제 해결 방법론이므로 수학 문제를 프로그래밍으로 해결하는 데 있어서 상당한 이득을 볼 수 있다.
