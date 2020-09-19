# React 기본 개념

## 컴포넌트 만들기

```js
// Hello.js
import React from "react";

function Hello() {
  return <div>안녕하세요</div>;
}

export default Hello;
```

- React 컴포넌트를 만들 땐 `import React from "react";`를 통해 React를 불러와야 한다.
- 컴포넌트는 함수, 클래스 형태로도 작성할 수 있다.
- 컴포넌트를 내보내기 위해선 `export default Hello;` 코드를 작성해야 한다.

```js
// App.js
import React from "react";
import Hello from "./Hello";

function App() {
  return (
    <div>
      <Hello />
    </div>
  );
} // 컴포넌트 불러오기

export default App;
```

## JSX

JSX는 React에서 사용되는 문법이다. HTML처럼 생겼지만 JS로 기능한다.

```js
<div>
  <h1>Hello World!</h1>
</div>; // 코드 작성

React.createElement(
  "div",
  null,
  /*#__PURE__*/ React.createElement("h1", null, "Hello World!")
); // babel 변환
```

- React 컴포넌트 파일에서 XML 형태로 코드를 작성하면 babel이 JSX를 JS로 변환해준다.
- JSX가 JS로 제대로 변환이 되려면 몇 가지 규칙을 지켜주어야 한다.

1. 꼭 닫혀야 하는 태그

```js
function App() {
  return (
    <div>
      <Hello />
      <input />
      <br />
    </div>
  );
}
```

- 태그 사이에 내용이 들어가지 않을 때에는 Self Closing 태그를 사용해야 한다.

2. 꼭 감싸져야 하는 태그

```js
function App() {
  return (
    // <div>
        <Hello />
        <div>Bye.</div>
    //</div>
  );
}
```

- 위와 같이 작성하면 에러가 발생한다.
- 전체를 div로 감싸거나 div를 사용하기 애매할 때, React의 Fragment 라는 것을 사용하면 된다.

```js
function App() {
  return (
    <>
      <Hello />
      <div>안녕히계세요</div>
    </>
  );
}
```

- 태그를 작성할 때 이름 없이 작성을 하면 Fragment가 만들어지는 데, 브라우저 상에서 별도의 엘리먼트로 나타나지 않는다.

3. JSX 안에 JS 값 사용하기

```js
function App() {
  const name = "react";
  return (
    <>
      <Hello />
      <div>{name}</div>
    </>
  );
}
```

- JSX 내부에 JS 변수를 보여줘야 할 때는 `{}`로 감싸서 보여준다.

4. style과 className

```js
function App() {
  const name = "react";
  const style = {
    backgroundColor: "black",
    color: "aqua",
    fontSize: 24, // 기본 단위 px
    padding: "1rem", // 다른 단위 사용 시 문자열로 설정
  };

  return (
    <>
      <Hello />
      <div style={style}>{name}</div>
      <div className="gray-box"></div>
    </>
  );
}
```

- JSX에서 태그에 `style`과 CSS class를 설정하는 방법은 HTML에서와는 다르다.
- 인라인 스타일은 객체 형태로 작성해야 하며, `background-color` 등과 같이 `-`로 구분된 이름은 camelCase 형태로 네이밍해야 한다.
- CSS class를 설정할 때는 `class=`가 아닌 `className=`으로 설정해야 한다.

5. 주석

- JSX에서 주석은 `{/* 주석 처리 */}` 형태로 작성한다.
- 열리는 태그 내부에서는 `// 주석 처리` 형태도 가능하다.
