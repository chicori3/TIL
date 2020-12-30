# useNetwork

```js
const useNetwork = (onChange) => {
  const [status, setStatus] = useState(navigator.onLine); // true 또는 false
  const handleChange = () => {
    if (typeof onChange === "function") {
      // onChange가 함수일 경우
      onChange(navigator.onLine);
    }
    setStatus(navigator.onLine);
  };
  useEffect(() => {
    window.addEventListener("online", handleChange);
    window.addEventListener("offline", handleChange);
    return () => {
      // componentWillUnmount 일 때 이벤트 제거
      window.removeEventListener("online", handleChange);
      window.removeEventListener("offline", handleChange);
    };
  }, []);
  return status;
};

const App = () => {
  const handleNetworkChange = (online) => {
    console.log(onLine ? "Online" : "Offline");
  };
  const onLine = useNetwork(handleNetworkChange);
  return (
    <div class="App">
      <h1>{onLine ? "Online" : "Offline"}</h1>
    </div>
  );
};
```

- `useNetwork`는 온라인, 오프라인 상태를 감지하는 Hook이다.
