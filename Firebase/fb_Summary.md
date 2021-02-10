# Firebase

- [Link](https://firebase.google.com/?hl=ko)
- 웹 사이트를 통해 제공해주는 백엔드 서비스

## BaaS

- `BaaS`는 Backend as a Service의 약자이다.
- 백엔드 기능을 클라우드 서비스 형태로 제공한다.
- 데이터 베이스, 소셜 서비스 연동, 파일 시스템 등을 API 형태로 제공해준다.

## 시작하기

```
yarn add firebase
```

```js
// firebase.js
import firebase from "firebase";
import "firebase/firestore";

const firebaseConfig = {
  // config
  apiKey: "API_KEY",
  authDomain: "PROJECT_ID.firebaseapp.com",
  databaseURL: "https://PROJECT_ID.firebaseio.com",
  projectId: "PROJECT_ID",
  storageBucket: "PROJECT_ID.appspot.com",
  messagingSenderId: "SENDER_ID",
  appId: "APP_ID",
  measurementId: "G-MEASUREMENT_ID",
};

// 초기화
firebase.initializeApp(firebaseConfig);

const firestore = firebase.firestore();

export { firestore };

```

## 사용하기

```js
// firebase.js
export const authService = firebase.auth();
export const database = firebase.database();
```

필요한 경우 `firebase.something()`을 components 내에서 호출 해야하는 데,        
이런 식으로 작성하면 단 한 번만 호출해서 사용할 수 있다.
