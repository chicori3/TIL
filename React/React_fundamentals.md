# React Fundamentals

리액트에서 자주 쓰이는 컨셉 또는 문법에 대해 알아보자.

## [Arrow Function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)

```js
const materials = ["Hydrogen", "Helium", "Lithium", "Beryllium"];

console.log(materials.map((material) => material.length));
// expected output: Array [8, 6, 7, 9]
```

1. 기본적으로 Arrow Function은 return이 함축되어 있다.
2. argument가 하나라면 괄호가 없어도 되지만, 두 개 이상이라면 필요하다.
3. function 표현식에 비해 구문이 짧고 간결하다.

## [Template Literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

```js
const name = "Saul";

console.log(`Better Call ${name}!`);

let a = 10;
let b = 5;
let c = "중학생";

console.log(`저는 ${a + b} 살이고 ${c}입니다.`);

const template = `
<ul class="nav">
<li class="Home"></li>
<li class="News"></li>
<li class="Contact"></li>
</ul>
`;

console.log(template);
```

1. 기존 방식처럼 + 연산자를 사용하지 않고 변수를 연결할 수 있고, 연산도 가능하다.
2. `|n` 을 사용하지 않고 줄바꿈을 할 수 있다.

## [Destructuring](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

```js
// Array Destructuring
const arr = [1, 2, 3];

const [one, two, three] = arr;

console.log(one, two, three); // 1, 2, 3

// Object Destructuring
const human = {
  name: "saul",
  lastName: "goodman",
  country: "america",
  favFood: {
    lunch: "sushi",
    dinner: "only coffee",
  },
};

// const name = human.name
// const lastName = human.lastName
// const difName = human.country
// const dinner = human.favFood.dinner

const {
  name,
  lastName,
  country: difName,
  favFood: { lunch, dinner },
} = human;

console.log(name, lastName, difName, lunch, dinner);
```

1. Array destructuring은 배열의 각 요소를 배열의 인덱스로부터 추출하여 변수 리스트에 할당한다.
1. Array destructuring을 위해서는 할당 연산자 왼쪽에 배열 형태의 변수 리스트가 필요하다.
1. Object destructuring은 객체의 각 프로퍼티를 객체로부터 추출하여 변수 리스트에 할당한다.
1. `country: difName` 은 변수의 이름을 바꿔서 저장하고, `favFood:{}`는 해당 객체의 안으로 들어가는 것이다.

## [Spread Operator](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

```js
const days = ["Mon", "Tue", "Wed"];
const otherDays = ["Thu", "Fri", "Sat"];

const allDays = days + otherDays;
console.log(allDays); // 전부 String으로 변환된다. "Mon,Tue,WedThu, Fri, Sat"

let solution = [...days, ...otherDays];
console.log(solution); // Array ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

1. Spread Operator는 배열이나 문자열로부터 요소를 가져온다.
1. 인자나 함수에서도 사용할 수 있고, 여러 개의 Object나 배열, 복사본을 만들 때 사용한다.
