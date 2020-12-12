# useTabs

```js
// 예제에 사용할 tab
const content = [
  {
    tab: "Section 1",
    content: "I am the content 1",
  },
  {
    tab: "Section 2",
    content: "I am the content 2",
  },
];

// map()을 사용하여 배열을 버튼으로 만들기
const App = () => {
  return (
    <div class="App">
      {content.map((section) => (
        <button>{section.tab}</button>
      ))}
    </div>
  );
};
```

```js
// useTabs Hook 만들기
const useTabs = (initialTab, allTabs) => {
  const [currentIndex, setCurrentIndex] = useState(initialTab); // useState에 initialTab을 초기값으로 세팅
  return {
    currentItem: allTabs[currentIndex], // allTabs의 인덱스 값으로 찾은 현재 탭의 정보
    changeItem: setCurrentIndex, // 활성화 된 tab
  };
};

// onClick()을 사용하여 버튼 변경하기
const App = () => {
  const { currentItem, changeItem } = useTabs(0, content);
  return (
    <div className="App">
      {content.map((section, index) => (
        <button onClick={() => changeItem(index)}>{section.tab}</button>
      ))}
      <div>{currentItem.content}</div>
    </div>
  );
};
```

- `onClick` 이벤트가 발생하면 changeItem(index)가 실행되어 0 또는 1이 된다.
- `setCurrentIndex`의 item이 변경되며 state 또한 변경된다.
- state가 변경되며 `currentIndex`의 값이 바뀌게 된다.

```js
// 에러 잡기
const useTabs = (initialTab, allTabs) => {
  if (!allTabs || !Array.isArray(allTabs)) {
    return; // allTabs가 false 또는 배열이 아닐 경우 return
  }
  const [currentIndex, setCurrentIndex] = useState(initialTab);
  return {
    currentItem: allTabs[currentIndex],
    changeItem: setCurrentIndex,
  };
};
```
