# TypeScript

- Javascript에 Type을 표기할 수 있는 superset.
- 개발자의 실수를 줄여주고 더 좋은 코드를 짜도록 도와준다.

```ts
// 예시
const plus = (a: number, b: number) => a + b;

console.log(plus("String", 2)); // Error

let Hello: string = "hello";

Hello = 4; // Error

const greet = (name: string, age: number): string => {
  // String으로 return
  return `I am ${name} and ${age} years old.`;
};

console.log(greet("saul", 34));
```

## Why TypeScript?

- JS는 타입 시스템이 없는 동적 언어로 약한 타입 언어이다.
- TS는 JS에 타입 시스템을 적용해 대부분의 에러를 코드를 작성하는 중에 발견할 수 있다.

## Function of TS

- 크로스 플랫폼 지원: JS가 구동되는 모든 플랫폼에서 사용 가능
- 객체 지향 언어
- 정적 타입
- DOM 제어
- 최신 ECMAScript 지원

## Install

```zsh
yarn add typescript
```

- 이후 터미널에 `tsc`를 입력하면 TS를 자동으로 TS로 변환해준다.

## Compiler option

```ts
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES2015",
    "sourceMap": true
  },
  "include": ["index.ts"],
  "exclude": ["node_moduels"]
}
```

- tsconfig 파일로 컴파일러 옵션을 관리할 수 있다.
- `include`, `exclude` 옵션으로 포함할 경로와 제외할 경로를 설정할 수 있다.
