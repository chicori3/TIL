# 조건부 렌더링

특정 조건에 따라 다른 결과물을 렌더링 하는 것.

```js
// App.js
function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" isSpecial={true} />
      <Hello color="pink" />
    </Wrapper>
  );
}
```

- `true`는 JS값이기에 중괄호로 감싼다.

```js
// Hello.js
function Hello({ color, name, isSpecial }) {
  return (
    <div style={{ color }}>
      {isSpecial ? <b>*</b> : null}
      안녕하세요 {name}
    </div>
  );
}

Hello.defaultProps = {
  name: "이름없음",
};
```

- 삼항연산자를 이용해 `true` `false`에 따라 다른 결과값을 내게 한다.
- `isSpecial`의 값이 `true`라면 `<b>*</b>`를, 아니라면 `null`을 나타내게 했다.
- JSX에서 `null`, `false`, `undefined`를 렌더링하게 되면 아무것도 나타나지 않는다.

```js
// Hello.js
function Hello({ color, name, isSpecial }) {
  return (
    <div style={{ color }}>
      {isSpecial && <b>*</b>}
      안녕하세요 {name}
    </div>
  );
}

Hello.defaultProps = {
  name: "이름없음",
};
```

- 조건이 단순히 `true`면 보여주고 `false`면 숨긴다라면 `&&`을 쓰는 것이 더 편하다.

## Props 값 설정을 생략하면 ={true}

컴포넌트의 props 값 설정을 생략하면 이를 `true`로 설정한 것으로 간주한다.

```js
function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" isSpecial />
      <Hello color="pink" />
    </Wrapper>
  );
}
```

- `isSpecial`만 넣어도 `isSpecial={true}`와 같은 의미가 된다.
