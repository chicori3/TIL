# React Fundamentals

## 1. [Arrow Function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)

```js
const materials = ["Hydrogen", "Helium", "Lithium", "Beryllium"];

console.log(materials.map((material) => material.length));
// expected output: Array [8, 6, 7, 9]
```

1. 기본적으로 Arrow Function은 return이 함축되어 있다.
2. argument가 하나라면 괄호가 없어도 되지만, 두 개 이상이라면 필요하다.
3. function 표현식에 비해 구문이 짧고 간결하다.

## 2. [Template Literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

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
