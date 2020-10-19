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

- IState는 인터페이스로 TS에서 타입을 설정하는 기능을 한다.
- state와 props를 가진 클래스형 컴포넌트는 `<{props},{state}>`를 작성해주어야 한다.
- 컴포넌트에 IState를 추가하여 counter는 number 타입임을 TS에 알려준다.

## React Props with TS

```js
// Number.tsx
interface IProps {
  count: number;
}

const Number: React.FunctionComponent<IProps> = ({ count }) => (
  <Container>{count}</Container>
);

// App.tsx
class App extends Component<{}, IState> {
  state = {
    counter: 0,
  };
  render() {
    const { counter } = this.state;
    return (
      <div>
        {counter}
        <Number count={counter} /> <button onClick={this.add}>ADD</button>
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
```

- Number 컴포넌트는 함수형 컴포넌트로 `React.FunctionComponent<>`로 작성하며 괄호 안에는 인터페이스를 적는다.
- count는 인터페이스에서 number로 타입을 설정해주었다.
