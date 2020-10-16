# React with TS

## 프로젝트 생성

- 새로 생성
  `$ yarn create=react-app my-app --typescript`

- 프로젝트에 TS 추가
  `$ yarn create react-app my-app --template typescript`

## React State with TS

```js
// App.tsx
interface IState {
  counter: number; // 인터페이스 설정
}

class App extends Component<{}, IState> {
  // State 전달
  state = {
    counter: 0,
  };
  render() {
    const { counter } = this.state;
    return (
      <div>
        {counter} <button onClick={this.add}>Add</button>
      </div>
    );
  }
  add = () => {
    this.setState((prev) => {
      return {
        counter: prev.counter + 1,
      };
    });
  };
}
```

- IState는 number 타입을 가지고 있다.
- Component에 IState를 추가하여 counter는 number 타입임을 TS에 알려준다.
