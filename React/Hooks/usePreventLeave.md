# usePreventLeave

`useState`와 `useEffect`를 사용하지 않는 함수형 컴포넌트로 Hook은 아니다.

```js
const usePreventLeave = () => {
  const listener = (event) => {
    event.preventDefault(); // 이벤트를 중지시키는 메서드
    event.returnValue = "";
  };
  const enablePrevent = () => window.addEventListener("beforeunload", listener); // 이벤트 추가
  const disablePrevent = () =>
    window.removeEventListener("beforeunload", listener); // 이벤트 제거
  return { enablePrevent, disablePrevent };
};

const App = () => {
  const { enablePrevent, disablePrevent } = usePreventLeave();
  return (
    <div class="App">
      <button onClick={enablePrevent}>Protect</button>
      <button onClick={disablePrevent}>unProtect</button>
    </div>
  );
};
```

- `usePreventLeave`는 브라우저를 닫기 전에 confirm 창을 띄워 확인 받는 함수이다.
- `beforeunload`는 브라우저가 닫히기 전에 함수를 실행되게 한다.
