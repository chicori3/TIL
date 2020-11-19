# React Props

## props를 통해 컴포넌트에 값 전달하기

1. props 기본 사용법

```js
// App.js
function App() {
  return <Hello name="react" />;
}

// Hello.js
function Hello(props) {
  return <div>Hello {props.name}</div>;
}
```

- props는 properties의 줄임말로 어떤 값을 컴포넌트에 전달해야할 때, props를 사용한다.
- 컴포넌트에게 전달되는 props는 파라미터를 통해 조회가 가능하다.
- props는 객체 형태로 전달되며, `name` 값을 조회하고 싶다면 `props.name`을 조회하면 된다.

2. 여러개의 props, 비구조화 할당

```js
// App.js
function App() {
  return <Hello name="react" color="red" />;
}

// Hello.js
function Hello({ color, name }) {
  return <div style={{ color }}>안녕하세요 {name}</div>;
}
```

3. defaultProps로 기본값 설정

```js
// Hello.js
function Hello({ color, name }) {
  return <div style={{ color }}>Hello {name}</div>;
}

Hello.defaultProps = {
  name: "noName",
};

// App.js
function App() {
  return (
    <>
      <Hello name="react" color="red" />
      <Hello color="pink" />
    </>
  );
}
```

4. props.children

```js
// Wrapper.js
function Wrapper({ children }) {
  const style = {
    border: "2px solid black",
    padding: "16px",
  };
  return <div style={style}>{children}</div>;
}

// App.js
function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" />
      <Hello color="pink" />
    </Wrapper>
  );
}
```

- 컴포넌트 태그 사이에 넣은 값을 조회하고 싶을 때, `props.children`을 조회하면 된다.
