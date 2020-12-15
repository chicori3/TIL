# useEffect

```js
const App = () => {
  const sayHello = () => console.log("hello");

  const [number, setNumber] = useState(0);
  const [anumber, setaNumber] = useState(0);

  useEffect(() => sayHello()); // 인자가 없을 때는 모든 변화에 작동한다

  useEffect((sayHello, [number])); // sayHello Effect가 number가 변화한 경우에만 작동한다

  return (
    <div className="App">
      <div>Hi</div>
      <button onClick={() => setNumber(number + 1)}>{number}</button>
      <button onClick={() => setaNumber(anumber - 1)}>{anumber}</button>
    </div>
  );
};
```

- `useEffect`는 `componentDidMount`,`componentDidUpdate`, `componentWillUnmount`가 합쳐진 것과 같게 생각하면 된다.
- `useEffect`는 어떤 효과를 줄 것인지에 대한 함수형의 effect를 첫 번째 인자로 받는다.
- 두 번째 인자는 dependency로 deps가 있다면 deps의 리스트에 있는 값일 때만 effect가 실행된다.
- 렌더링 이후에 effect를 사용하지 않고 싶은 경우에는 빈 배열 []을 인자로 주면 된다.
