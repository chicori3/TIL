# useState

```js
// 버튼을 클릭하면 값이 변하는 예시
import React, { useState } from "react";

export default function App() {
  // Hook 작성
  const [item, setItem] = useState(1);
  // useState는 2개의 value를 Array로 return한다.
  const incrementItem = () => {
    setItem(item + 1);
  };
  const decrementItem = () => {
    setItem(item - 1);
  };
  return (
    <div class="App">
      <h1>{item}</h1>
      <button onClick={incrementItem}>Increment</button>
      <button onClick={decrementItem}>decrement</button>
    </div>
  );
}
```

- `useState`는 state를 함수 컴포넌트 안에서 사용할 수 있게 한다.
- `useState`는 현재의 state 값 `item`과 값을 업데이트하는 `setItem`을 파라미터로 사용한다. 이름은 상관없다.
- `useState`를 호출하여 사용할 수 있고, class의 `this.setState`와는 다르게 이전 state와 새로운 state를 합치지 않는 차이가 있다.

```js
// 여러 state 변수 선언 예시
function ExampleWithManyStates() {
  // 상태 변수를 여러 개 선언
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState("banana");
  const [todos, setTodos] = useState([{ text: "Learn Hooks" }]);
  // ...
}
```
