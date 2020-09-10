# NodeJS?

- NodeJS는 구글 크롬의 자바스크립트 엔진(V8 Engine)으로 빌드 된 Javascript 런타임이다.
- Javascript를 브라우저의 밖으로 확장하기 위해 만들어졌다.
- [Express](https://expressjs.com/ko/)와 같은 라이브러리를 이용해 서버를 만들 수 있지만, NodeJs 자체는 웹 서버가 아니다.

## 1. NodeJS의 특징

### 비동기 I/O 처리

- NodeJS 라이브러리의 모든 API는 비동기식이다.
- NodeJS 기반 서버는 API가 실행되었을 때, 데이터를 반환할 때 까지 기다리지 않고 다음 API를 실행한다.
- 이전의 실행한 API가 결과값을 반환할 시, NodeJS의 이벤트 알림 메커니즘을 통해 결과값을 받아온다.

### 빠른 속도

- 구글 크롬의 V8 자바스크립트 엔진을 사용하여 빠른 코드 실행을 제공한다.

### 단일 쓰레드와 뛰어난 확장성

- NodeJS는 이벤트 루프와 함께 단일 쓰레드 모델을 제공한다.
- 이벤트 메커니즘은 서버가 멈추지 않고 반응하도록 하여 서버의 확장성을 키운다.
- 일반적인 웹 서버보다 훨씬 많은 요청을 처리할 수 있다.

### 노 버퍼링

- NodeJS 어플리케이션에는 데이터 버퍼링이 없고, 데이터를 chunk로 출력한다.

### 라이센스

- NodeJS는 MIT License가 적용되어 있다.

## 2. NodeJS를 사용하기 적합한 예

- 입출력이 잦은 어플리케이션
- 데이터 스트리밍 어플리케이션
- 데이터를 실시간으로 다루는 어플리케이션
- JSON API 어플리케이션
- 싱글페이지 어플리케이션

## 3. NodeJS를 사용하기 적합하지 않은 예

- 복잡한 데이터를 처리하기 위해 하드웨어를 사용해야 하는 곳에는 Django가 적합하다

## 4. 설치

```
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_14.x | bash -
apt-get install -y nodejs
```
