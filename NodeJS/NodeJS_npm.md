# Node Package Manager(npm)

- npm은 자바스크립트 패키지 매니저이다.
- Node.js에서 사용할 수 있는 모듈들을 패키지화하여 모아둔 저장소 겸 패키지 설치 및 관리를 위한 CLI(Command line interface)를 제공한다.

## 1. 버전 확인

- Node.js를 설치하면 npm이 같이 설치된다.
- `$ node -v`를 터미널에 입력하면 버전을 알려준다.
- 최신 버전, 안정 버전을 설치할 땐 다음을 입력한다.

```bash
$ n latest // 최신 버전
$ n stable // 안정 버전
$ n lts // 오랜 기간동안 사용할 수 있도록 지원하는 안정 버전
```

- 특정 버전을 설치할 땐 버전을 같이 입력한다.

```bash
$ n 0.8.14
$ n 0.10.12
```

- 여러가지 버전이 설치되어 있을 때 버전을 변경하려면 `n`을 입력한다.
- 버전을 선택해서 삭제하거나, 현재 버전 외에 모든 버전을 삭제할 수 있다.

```bash
$ n rm 0.8.14 // 선택 삭제
$ n prune // 현재 버전 외에 전체 삭제
```

- `$ npm -v` 를 입력하면 npm의 버전을 알려준다.
- npm 재설치, 업데이트를 할 땐 다음을 입력한다.

```bash
$ sudo npm install -g npm
```

## 2. npm을 이용하여 모듈 설치하기

- `$ npm install <package>`를 입력하면 설치된다.
- 설치하면 다음과 같이 이용할 수 있다.

```js
const express = require("express");
```

## 3. 글로벌과 로컬

- 글로벌은 시스템 디렉토리, 로컬은 명령어를 실행한 디렉토리의 node_module을 말하며 npm은 기본적으로 로컬 모드로 설치한다.
- 글로벌 모드로 설치했을 경우에는 바로 require 할 수 없고 npm link를 입력해서 해당 모듈을 호출할 수 있다.

```bash
$ npm install -g express
$ cd [local path]/project
$ npm link express
```

## 4. package.json

- package.json은 node 어플리케이션 / 모듈의 경로에 위치하며 패키지의 속성을 정의한다.
- git을 통해 관리할 때 node_modules 까지 push 하지 않기에 repo를 clone을 받는다면 모듈 설치를 해야한다.
- `$ npm init`을 통해 package.json을 생성한다.
- package.json이 관리되면 git clone 후에 또는 node_modules가 존재하지 않을 경우 `$ npm install`을 이용하여 설치할 수 있다.

## 5. 모듈 관리

1. 모듈 제거

```bash
$ npm uninstall express
```

2. 모듈 업데이트

```bash
$ npm update express
```

3. 모듈 검색

```bash
$ npm search express
```
