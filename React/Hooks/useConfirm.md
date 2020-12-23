# useConfirm

`useState`와 `useEffect`를 사용하지 않는 함수형 컴포넌트로 Hook은 아니다.

```js
const useConfirm = (message = "", onConfirm, onCancle) => {
  if (!onConfirm || typeof onConfirm !== "function") {
    // onConfirm이 없거나 함수가 아니라면 return
    return;
  }
  const confirmAction = () => {
    // 응답에 따른 이벤트 실행 함수
    if (confirm(message)) {
      onConfirm(0);
    } else {
      onCancle();
    }
  };
  return confirmAction();
};

const App = () => {
  const del = () => console.log("del");
  const abort = () => console.log("aborted");
  const confirmDel = useConfirm("sure?", del, abort); // useConfirm의 인자
  return (
    <div class="App">
      <button onclick={confirmDel}>Del</button>
    </div>
  );
};
```

- `useConfirm`은 사용자에게 확인을 받는 기능을 하는 함수로 사용자가 저장하거나 삭제할 때 활용할 수 있다.
- brower가 이벤트를 실행하기 전에 confirm을 우선 실행하고, `onConfirm`이나 `onCancle`이 실행된다.
