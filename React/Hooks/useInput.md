# useInput

```js
// input에 초기값 설정하기
const useInput = (initialValue) => {
  const [value, setValue] = useState(initialValue);
  return { value };
};

const App = () => {
  const name = useInput("Mr.");

  return (
    <div class="App">
      <h1>Hi</h1>
      <input
        placeholder="Name"
        {...name} // value={name.value}와 같다
      />
    </div>
  );
};
```

- `useInput`은 input을 업데이트한다.
- input의 초기값으로 "Mr."가 return 된다.

```js
// 검증요소 추가하기
const useInput = (initialValue, validator) => {
  // 1. validator는 매번 바뀐다
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    const {
      target: { value },
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(value); // 2. validator 함수(maxLength)를 검증한다.
    }
    if (willUpdate) {
      setValue(value); // 3. true를 받으면 업데이트한다
    }
  };
  return { value, onChange };
};

const App = () => {
  const maxLength = (value) => value.length <= 10; // 길이를 검증하여 boolean을 return 하는 함수
  const name = useInput("Mr.", maxLength);

  return (
    <div class="App">
      <h1>Hi</h1>
      <input
        placeholder="Name"
        {...name} // value={name.value}와 같다
      />
    </div>
  );
};
```
