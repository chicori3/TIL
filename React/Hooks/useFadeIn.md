# useFadeIn

```js
const useFadeIn = (duration = 1, delay = 0) => {
  if (typeof duration !== "number" || typeof delay !== "number") {
    return; // 검증
  }
  const element = useRef(); // useRef = document.querySelector
  useEffect(() => {
    if (element.current) {
      const { current } = element;
      current.style.transition = `opacity ${duration}s ease-in-out ${delay}s`;
      current.style.opacity = 1;
    }
  }, []);
  return { ref: element, style: { opacity: 0 } };
};

const App = () => {
  const fadeInH1 = useFadeIn(2, 1);
  const fadeInP = useFadeIn(5, 3);
  return (
    <div class="App">
      <h1 {...fadeInH1}>Hi</h1>
      <p {...fadeInP}>lorem ipsum </p>
    </div>
  );
};
```

- 어떤 요소를 시간이 지남에 따라 나타나게 하는 hook
