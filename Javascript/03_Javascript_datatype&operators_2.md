## 5. 배열

배열은 자바스크립트 객체의 특별한 형태다. C나 자바의 배열과 같은 기능을 하는 객체지만, 이들과는 다르게 굳이 크기를 지정하지 않아도 되며, 어떤 위치에 어느 타입의 데이터를 저장하더라도 에러가 발생하지 않는다.

## 5-1. 배열 리터럴

- **배열 리터럴**은 자바스크립트에서 새로운 배열을 만드는 데 사용하는 표기법이다.
- 배열 리터럴은 **대괄호[]**를 사용한다.
- 배열 리터럴에서는 **각 요소의 값**만을 포함한다.
- 객체가 **프로퍼티의 이름**으로 해당 프로퍼티에 접근했다면, 배열은 **배열 내 위치 인덱스값**을 넣어서 접근한다.
- 배열 내의 첫 번째 원소는 인덱스 0부터 시작한다.

```javascript
// 배열 리터럴을 통한 5개 원소를 가진 배열 생성
var colorArr = ["orange", "yellow", "blue", "green", "red"];
console.log(colorArr[0]); // orange
console.log(colorArr[1]); // yellow
console.log(colorArr[4]); // red
```

## 5-2. 배열의 요소 생성

객체가 동적으로 프로퍼티를 추가할 수 있듯이, 배열도 동적으로 배열 원소를 추가할 수 있다. 특히, 자바스크립트의 배열의 경우는 값을 순차적으로 넣을 필요 없이 아무 인덱스 위치에나 값을 동적으로 추가할 수 있다.

```javascript
// 빈 배열
var emptyArr = [];
console.log(emptyArr[0]); // undefined -01-

// 배열 요소 동적 생성
emptyArr[0] = 100;
emptyArr[3] = "eight";
emptyArr[7] = true;
console.log(emptyArr); // [100, undefined * 2, 'eight', undefined * 3, true]
console.log(emptyArr.length); // 8 -02-
```

- 1.  배열 리터럴에서 대괄호만을 사용할 경우, emptyArr처럼 빈 배열이 생성된다. emptyArr는 요소가 없는 빈 배열이므로, emptyArr[0]와 같이 배열 원소에 접근해도 값이 없는 undefined 값이 출력된다. 이것은 배열 또한 자바스크립트 객체이기 때문에 객체에서도 포함되지 않은 객체의 프로퍼티에 접근한 경우 undefined가 출력된 것과 같이 배열의 경우도 값이 없는 원소에 접근할 경우 undefined가 출력되는 것이다.
- 2.  배열의 요소는 숫자나 문자열 같은 기본 타입의 값들을 포함해서, 객체나 함수, 배열 등과 같이 자바스크립트의 모든 데이터 타입의 값을 포함할 수 있다. 여기서 특이한 점은 3개의 요소 값만을 할당했지만, 8개의 배열 요소값이 출력된다는 것이다. **이것은 자바스크립트가 배열의 크기를 현재 배열의 인덱스 중 가장 큰 값을 기준으로 정하기 때문이다.** 현재 배열의 인덱스 중 가장 큰 값은 7이므로 총 배열의 개수는 0부터 7까지 총 8개가 되는 것이다. 자바스크립트의 **모든 배열은 이러한 length 프로퍼티**가 있으며, 이것은 배열의 동작을 이해하는 데 아주 중요하다.

## 5-3. 배열의 length 프로퍼티

자바스크립트의 모든 배열은 **length 프로퍼티**가 있다. length 프로퍼티는 배열의 원소 개수를 나타내지만, 실제로 배열에 존재하는 원소 개수와 일치하는 것은 아니다. length 프로퍼티는 **배열 내 가장 큰 인덱스에 1을 더한 값**이다.

```javascript
var arr = [];
console.log(arr.length); // 0

arr[0] = 0; // arr.length = 1
arr[1] = 1; // arr.length = 2
arr[2] = 2; // arr.length = 3
arr[100] = 100;
console.log(arr.length); // 101
```

동적으로 배열 원소에 값을 저장할수록 가장 큰 인덱스 값의 length 값이 늘어난다. 하지만 실제 메모리는 length 크기처럼 할당되지 않는다.

```javascript
var arr = [0, 1, 2];
console.log(arr.length); // 3

arr.length = 5;
console.log(arr); // [0, 1, 2, undefined * 2]

arr.length = 2;
console.log(arr); // [0, 1]
console.log(arr[2]); // undefined
```

length 프로퍼티를 벗어나는 실제 값은 삭제된다.

### 5-3-1. 배열 표준 메서드와 length 프로퍼티

자바스크립트는 배열에서 사용 가능한 다양한 표준 메서드를 제공한다. 이러한 배열 메서드는 **length 프로퍼티**를 기반으로 동작하고 있다.
[push()메서드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/push)는 인수로 넘어온 항목을 배열의 끝에 추가하는 자바스크립트 표준 배열 메서드다. 이 메서드는 배열의 현재 length 값의 위치에 새로운 원소값을 추가한다. 배열의 length 프로퍼티는 '현재 배열의 맨 마지막 원소의 인덱스 +1'을 의미하므로 결국 length 프로퍼티가 가리키는 인덱스에 값을 저장하는 것은 배열의 끝에 값을 추가하는 것과 같은 결과가 되기 때문이다.

```javascript
// arr 배열 생성
var arr = ["zero", "one", "two"];

// push() 메서드 호출
arr.push("three");
console.log(arr); // ['zero', 'one', 'two', 'three']

// length 값 변경 후, push() 메서드 호출
arr.length = 5;
arr.push("four");
console.log(arr); // ['zero', 'one', 'two', 'three', undefined, 'four']
```

## 5-4. 배열과 객체

자바스크립트에서는 배열 역시 객체다. 하지만 배열은 일반 객체와는 약간 차이가 있다.

```javascript
// colorsArray 배열 -01-
var colorsArray = ["oragne", "yellow", "green"];
console.log(colorsArray[0]); // orange

// colorsObj 객체
var colorsObj = { "0": "orange", "1": "yellow", "2": "green" };
console.log(colorsObj[1]); // yellow

// typeof 연산자 비교 -02-
console.log(typeof colorsArray); // object (not array)
console.log(typeof colorsObj); // object

// length 프로퍼티 -03-
console.log(colorsArray.length); // 3
console.log(colorsObj.length); // undefined

// 배열 표준 메서드 -04-
colorsArray.push("red"); // ["oragne", "yellow", "green", "red"];
colorsObj.push("red"); // Uncaught TypeError: Object #<Object> has no method 'push'
```

- 1. colorsArray 배열과 colorsObj 객체를 생성했다. 대괄호 안에는 접근하려는 프로퍼티의 속성을 **문자열 형태**로 적어야 하지만, 자바스크립트 엔진이 [] 연산자 내에 숫자가 사용될 경우, 해당 숫자를 자동으로 문자열 형태로 바꿔준다.
- 2. typeof 연산 결과는 배열과 객체 모두 **object**로 나온다.
- 3. 배열과 다르게 객체는 length 프로퍼티가 존재하지 않는다. 때문에 colorsObj.length의 값은 undefined가 출력된다.
- 4. 객체는 push()와 같은 **표준 배열 메서드**를 사용할 수 없다. 객체의 경우 **Object.prototype 객체**가 프로토타입이고, 배열의 경우 **Array.prototype 객체**가 프로토타입이 된다.

## 5.5. 배열의 프로퍼티 동적 생성

배열도 자바스크립트 객체이므로, 인덱스가 숫자인 배열 원소 이외에도 객체처럼 동적으로 프로퍼티를 추가할 수 있다.

```javascript
// 배열 생성
var arr = ["zero", "one", "two"];
console.log(arr.length); // 3

// 프로퍼티 동적 추가
arr.color = "blue";
arr.name = "number_array";
console.log(arr.length); // 3

// 배열 원소 추가
arr[3] = "red";
console.log(arr.length); // 4

// 배열 객체 출력
console.dir(arr);
```

arr 배열에 동적으로 color와 name 프로퍼티를 추가했지만 배열에 동적 프로퍼티가 추가될 경우는 length 값이 변하지 않는다. **배열의 length 프로퍼티는 배열 원소의 가장 큰 인덱스가 변했을 경우만 변경된다.** 배열도 객체처럼 key:value 형태로 배열 원소, 프로퍼티 등이 있다.

## 5-6. 배열의 프로퍼티 열거

객체는 for in 문으로 프로퍼티를 열거한다. 배열도 객체이므로 for in 문을 사용할 수 있지만, 불필요한 프로퍼티가 출력될 수 있으므로 되도록 for 문을 사용하는 것이 좋다.

```javascript
for (var prop in arr) {
  console.log(prop, arr[prop]);
} // 0 zero 1 one 2 two 3 red color blue name number_array

for (var i = 0; i < arr.length; i++) {
  console.log(i, arr[i]);
} // 0 "zero" 1 "one" 2 "two" 3 "red"
```

## 5-7. 배열 요소 삭제

배열도 객체이므로, 배열 요소나 프로퍼티를 삭제하는 데 delete 연산자를 사용할 수 있다. 그러나 delete 연산자는 해당 요소의 값을 undefined로 설정할 뿐 원소 자체를 삭제하지는 않는다. 때문에 보통 배열에서 요소들을 완전히 삭제할 경우 [splice() 배열 메서드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)를 사용한다.

```javascript
var arr = [0, 1, 2, 3];

arr.splice(2, 1); // 2번째 요소를 시작점으로 1개의 원소를 삭제한다.
console.log(arr); // [0, 1, 3]
console.log(arr.length); // 3
```
