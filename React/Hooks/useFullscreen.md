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
        <img src="../images/logo512.png" />
        <button onClick={exitFull}>exitFull</button>
        <button onClick={triggerFull}>triggerFull</button>
      </div>
    </div>
  );
};
```

- `useFullscreen`은 무언가를 전체화면으로 전환하는 hook이다.
