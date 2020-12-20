# useClick

```js
// useRef() 알아보기
const App = () => {
  const input = useRef(); // useRef() 선언
  setTimeout(() => input.current.focus(), 2000); // 2초 뒤에 함수 실행

  return (
    <div className="App">
      <div>Hello</div>
      <input
        ref={input} // 선언한 ref를 적용
        placeholder="place"
      />
    </div>
  );
};
```

- React의 모든 컴포넌트는 `reference element`를 가지고 있다.
- `reference`는 컴포넌트를 선택할 수 있는 방법으로 `document.getElementById()`와 비슷하다.
- `useRef()`로 Ref 객체를 만들고 선택하고 싶은 `DOM`에 `ref` 값으로 설정한다.

```js
// useClick() 사용하기
const useClick = (onClick) => {
  const element = useRef(); // 1. useRef() 선언
  useEffect(() => {
    if (element.current) {
      // componentDidMount, componentDidUpdate 일 때 실행
      element.current.addEventListener("click", onClick);
      // 3. element.current가 있다면 element.current에 함수를 실행하는 이벤트 생성
    }
    return () => {
      // componentWillUnmount 일 때 실행
      if (element.current) {
        element.current.removeEventListener("click", onClick);
      }
    };
  }, []); // dep가 없다면 update가 될 때마다 eventListener가 추가된다
  return element;
};

const App = () => {
  const sayHello = () => console.log("say hello"); // 4. 실행되는 함수
  const title = useClick(sayHello); // 2. 선언한 useRef()로 title 선택
  return (
    <div class="App">
      <h1 ref={title}>Hello</h1>
    </div>
  );
};
```
