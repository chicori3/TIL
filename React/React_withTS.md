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

## React Event with TS

```js
// Input.tsx
interface IInputProps {
  value: string;
  onChange: (event: React.SyntheticEvent<HTMLInputElement>) => void;
}

interface IFormProps {
  onFormSubmit: (event: React.FormEvent) => void;
}

export const Input: React.FunctionComponent<IInputProps> = ({
  value,
  onChange,
}) => (
  <input type="text" placeholder="Name" value={value} onChange={onChange} />
);

export const Form: React.FunctionComponent<IFormProps> = ({
  children,
  onFormSubmit,
}) => <form onSubmit={onFormSubmit}>{children}</form>;

// App.tsx
interface IState {
  counter: number;
  name: string; // name = {value}
}

class App extends Component<{}, IState> {
  state = {
    counter: 0,
    name: "", // name의 타입 = String
  };
  render() {
    const { counter, name } = this.state;
    return (
      <div>
        <Form onFormSubmit={this.onFormSubmit}>
          <Input value={name} onChange={this.onChange} />
        </Form>
        <Number count={counter} /> <button onClick={this.add}>ADD</button>
      </div>
    );
  }

  onChange = (event: React.SyntheticEvent<HTMLInputElement>) => {
    console.log(event.target);
  };

  onFormSubmit = (event: React.FormEvent) => {
    event.preventDefault();
  };
```

- Input에는 Input과 Form 함수형 컴포넌트를 만들고 App에는 onChange와 onFormSubmit 함수를 작성했다.
- 각 함수를 TS에 알려주기 위해 인터페이스에 `onChange: (event: React.SyntheticEvent<HTMLInputElement>) => void;`를 작성해주었는 데, onChange는 HTMLInputElement에 작동하는 SyntheticEvent이며 void를 리턴한다는 말이다.
- 타입이 정해진 함수를 사용할 App의 Form과 Input 컴포넌트에 작성한다.

## Styled Component with TS

```js
// Number.tsx

// interface IContainer {
//   isBlue: boolean;
// }

const Container =
  styled.span <
  { isBlue: boolean } >
  `
  color: ${(props) => (props.isBlue ? "blue" : "black")};
`;

const Number: React.FunctionComponent<IProps> = ({ count }) => (
  <Container isBlue={count > 10}>{count}</Container>
);
```

- styled component에 props를 추가할 수 있다.
- interface로도 작성할 수 있지만 그렇게 되면 너무 많은 interface를 관리해야 한다.
- 컴포넌트는 interface를, styled component는 인라인으로 작성하는 것이 깔끔하다.
