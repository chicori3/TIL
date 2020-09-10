# 02. Hello World

- 공식 문서 링크: https://nodejs.org/ko/docs/
- 시작 가이드: https://nodejs.org/ko/docs/guides/getting-started-guide/

## 1. 필요한 모듈 import 하기

- 어플리케이션에 필요한 모듈을 호출할 때 **require**를 사용한다.
- HTTP 모듈을 불러오고 반환되는 HTTP 인스턴스를 http 변수에 저장한다.

```javascript
const http = require("http");

const hostname = "127.0.0.1"; // localhost
const port = 3000; // 접근 포트
```

## 2. 서버 생성하기

- http 인스턴스를 사용하여 **http.createServer()** 메서드를 실행한다.
- **listen** 메서드를 사용하여 포트 3000과 bind한다.
- http.createServer()의 매개변수로 request, response를 매개변수로 가지고 있는 함수를 사용한다.
- 아래 코드는 "Hello World"를 리턴하는 포트 3000의 웹 서버를 생성해준다.

```javascript
const server = http.createServer((req, res) => {
  res.statusCode = 200; // http 응답 코드
  res.setHeader("Content-Type", "text/plain"); // 출력 내용 형태
  res.end("Hello World"); // Hello World 출력
});

server.listen(port, hostname, () => {
  // 127.0.0.1 호스트의 3000 포트로 들어오는 요청 대기
  console.log(`Server running at http://${hostname}:${port}/`); // 해당 이벤트 발생 시 터미널에 출력
});
```

## 3. 서버 테스트

```javascript
const http = require("http");

const hostname = "127.0.0.1";
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader("Content-Type", "text/plain");
  res.end("Hello World");
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

코드를 app.js에 작성한 후 서버를 실행시킨다.

```
$ node app.js
```

서버가 성공적으로 실행됐다면 터미널에 다음 텍스트가 출력된다.

```
Server running at http://127.0.0.1:3000/
```
