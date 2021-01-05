# useFullscreen

```js
const useFullscreen = (callback) => {
  const element = useRef();
  const runCb = (isFull) => {
    if (callback && typeof callback === "function") {
      callback(isFull);
    }
  };
  const triggerFull = () => {
    // 전체화면으로 전환
    switch (element.current) {
      case "element.current.requestFullscreen":
        // chrome, safari
        element.current.requestFullscreen();
      case "element.current.mozRequestFullScreen":
        // firefox
        element.current.mozRequestFullScreen();
      case "element.current.webkitRequestFullscreen":
        // opera
        element.current.webkitRequestFullscreen();
      case "element.current.msRequestFullscreen":
        // microsoft
        element.current.msRequestFullscreen();

      default:
        runCb(true);
    }
  };
  const exitFull = () => {
    // 전체화면을 해제
    document.exitFullscreen();
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    } else if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    } else if (document.msExitFullscreen) {
      document.msExitFullscreen();
    }
    runCb(false);
  };
  return { element, triggerFull, exitFull };
};

const App = () => {
  const onFullS = (isFull) => {
    // callback 함수
    console.log(isFull ? "Full" : "Small");
  };
  const { element, triggerFull, exitFull } = useFullscreen(onFullS);
  return (
    <div className="App">
      <h1>Hello</h1>
      <div ref={element}>
        <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9Ii0xMS41IC0xMC4yMzE3NCAyMyAyMC40NjM0OCI+CiAgPHRpdGxlPlJlYWN0IExvZ288L3RpdGxlPgogIDxjaXJjbGUgY3g9IjAiIGN5PSIwIiByPSIyLjA1IiBmaWxsPSIjNjFkYWZiIi8+CiAgPGcgc3Ryb2tlPSIjNjFkYWZiIiBzdHJva2Utd2lkdGg9IjEiIGZpbGw9Im5vbmUiPgogICAgPGVsbGlwc2Ugcng9IjExIiByeT0iNC4yIi8+CiAgICA8ZWxsaXBzZSByeD0iMTEiIHJ5PSI0LjIiIHRyYW5zZm9ybT0icm90YXRlKDYwKSIvPgogICAgPGVsbGlwc2Ugcng9IjExIiByeT0iNC4yIiB0cmFuc2Zvcm09InJvdGF0ZSgxMjApIi8+CiAgPC9nPgo8L3N2Zz4K" />
        <button onClick={exitFull}>exitFull</button>
        <button onClick={triggerFull}>triggerFull</button>
      </div>
    </div>
  );
};
```

- `useFullscreen`은 무언가를 전체화면으로 전환하는 hook이다.
