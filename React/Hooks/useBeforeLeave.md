# useBeforeLeave

```js
const useBeforeLeave = (onBefore) => {
  if (typeof onBefore !== "function") {
    // onBefore이 없거나 함수가 아니라면 return
    return;
  }
  const handle = (event) => {
    const { clientY } = event; // MouseeEvent = event
    if (clientY <= 0) {
      // 마우스의 좌표값이 0 이하
      onBefore();
    }
  };
  useEffect(() => {
    document.addEventListener("mouseleave", handle); // 컴포넌트가 마운트일 때 이벤트 추가
    return () => document.removeEventListener("mouseleave", handle); // 컴포넌트가 언마운트일 때 이벤트 제거
  }, []); // 이벤트를 한 번만 실행
};

const App = () => {
  const dontLeave = () => console.log("Dont leave");
  useBeforeLeave(dontLeave);
  return (
    <div class="App">
      <h1>Hi</h1>
    </div>
  );
};
```

- `useBeforeLeave`는 페이지를 벗어날 때 사용할 수 있는 Hook이다.
