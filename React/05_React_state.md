# React State & Life Cycle

## State

```js
import React from "react";

class App extends Component {
  state = { count: 0 };
  add = () => {
    // this.state.count = 1 // Dont this
    this.setState((current) => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState((current) => ({ count: current.count - 1 }));
  };
  render() {
    return (
      <div>
        <h1>The Number is:{this.state.count}</h1>
        <button onClick={this.add}>ADD</button>
        <button onClick={this.minus}>MINUS</button>
      </div>
    );
  }
}

export default App;
```

- state는 object이며 컴포넌트의 data가 들어갈 수 있고 또한 변한다.
- 변하는 data를 사용할 때 state를 이용한다.
- state의 data를 변경할 때는 직접 state를 변경하는 대신 setState를 사용해야 한다.
- 리액트는 setState가 실행되면 다시 render 한다.

## [Component Life Cycle](https://ko.reactjs.org/docs/react-component.html#mounting)

- Life Cycle(생명 주기)는 리액트가 Component를 생성하고 없애는 과정이다.

### Mount

컴포넌트의 인스턴스가 생성되어 DOM 상에 삽입될 때에 순서대로 호출된다.

1. constructor()

- 생성자 (construcutor)는 JS에서 class를 만들 때 호출된다.
- 생성자는 컴포넌트가 마운트 되기 전에 호출된다.
- this.state에 객체를 할당하여 지역 state를 초기화, 인스턴스에 이벤트 처리 메서드를 바인딩을 위해 사용한다.
- 생성자 내부에서 setState()를 호출하면 안 된다.

```js
// 해선 안 되는 작업
constructor(props) {
  super(props);
  // 여기서 this.setState()를 호출하면 안 됩니다!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}

constructor(props) {
 super(props);
 // 이렇게 하지 마세요!
 this.state = { color: props.color };
}
```

2. render()

- render()는 클래스 컴포넌트에서 반드시 구현되어야 한다.
- 리액트 엘리먼트, 배열, fragment, portal, string, number, boolean, null 중 하나를 반환해야 한다.
- 컴포넌트의 state를 변경하지 않고 동일한 결과를 반환할 수 있게 순수해야 한다.

3. componentDidMount()

- render()가 실행된 이후에 호출되는 메서드다.
- 외부에서 데이터를 불러올 때 요청을 보내기 적절하다.
- setState()를 즉시 호출하는 경우도 있다.

### Update

props 또는 state가 변경되면 갱신이 발생된다.

1. render()

2. componentDidUpdate()

- componentDidUpdate()는 갱신이 일어난 직후에 호출된다.
- 처음 렌더링할 때는 호출되지 않는다.
- setState()를 즉시 호출할 수도 있지만, 조건문으로 감싸지 않으면 무한 반복이 발생할 수 있다는 점에 주의해야 한다.

```js
componentDidUpdate(prevProps) {
  // 전형적인 사용 사례 (props 비교를 잊지 마세요)
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

### Unmount

컴포넌트가 DOM 상에서 제거될 때에 호출된다.

1. componentWillUnmount()

- componentWillUnmount()는 컴포넌트가 마운트 해제되어 제거되기 직전에 호출된다.
- 컴포넌트는 다시 렌더링 되지 않으므로, setState()를 호출하면 안 된다.

## 정리

```js
import React from "react";

class App extends React.Component {
  state = {
    count: 0,
  };
  add = () => {
    this.setState((current) => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState((current) => ({ count: current.count - 1 }));
  };
  // add나 minus 버튼을 누르면 update가 실행된다.
  componentDidMount() {
    console.log("Component rendered"); // render()가 호출된 후에 호출된다.
  }
  componentDidUpdate() {
    console.log("I just updated"); // 버튼을 누르면 호출된다.
  }
  componentWillUnmount() {
    console.log("I'm Done"); // 컴포넌트가 제거되어 호출되지 않는다.
  }
  render() {
    console.log("I'm rendering");
    // render는 생성자를 제외하고 가장 먼저 호출된다.
    // update가 되면 setState()를 호출하기 때문에 render()도 다시 호출된다.
    return (
      <div>
        <h1>The number is: {this.state.count}</h1>
        <button onClick={this.add}>Add</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    );
  }
}

export default App;
```
