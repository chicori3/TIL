# useTitle

```js
// useTitle 사용하기
const useTitle = (initialTitle) => {
  const [title, setTitle] = useState(initialTitle); // initialTitle를 초기값으로 설정
  const updateTitle = () => {
    const htmlTitle = document.querySelector("title");
    htmlTitle.innerText = title;
  };
  useEffect(updateTitle, [title]); // 컴포넌트가 마운트 될 때와 title이 업데이트 될 때, updateTitle 실행
  return setTitle; // 제목을 업데이트 하도록 setTitle을 return
};

const App = () => {
  const titleUpdater = useTitle("Loading..."); // App 컴포넌트에서 useTitle 함수 사용
  return (
    <div className="App">
      <div>Hi</div>
    </div>
  );
};
```

- App 컴포넌트가 마운트되며 선언한 `titleUpdater`의 "Loading..."이 title로 할당된다.
- `useEffect`가 `updateTitle`을 실행하여 title이 "Loading..."으로 바뀌게 된다.

```js
// setTimeout()을 이용해 title 업데이트
const useTitle = (initialTitle) => {
  const [title, setTitle] = useState(initialTitle);
  const updateTitle = () => {
    const htmlTitle = document.querySelector("title");
    htmlTitle.innerText = title;
  };
  useEffect(updateTitle, [title]);
  return setTitle;
};

const App = () => {
  const titleUpdater = useTitle("Loading...");
  setTimeout(() => {
    titleUpdater("Home");
  }, 2000); // 3초후 titleUpdater 실행
  return (
    <div className="App">
      <div>Hi</div>
    </div>
  );
};
```

- `setTimeout()` 메서드를 이용해 2초 후 "Home"을 `titleUpdater`의 새로운 인자로 넘긴다.
- title의 업데이트가 있으므로 `useEffect`가 실행되고 "Home"으로 title의 값이 변하게 된다.
