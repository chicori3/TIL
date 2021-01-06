# useNotification

```js
const useNotification = (title, options) => {
  if (!("Notification" in window)) {
    return; // window가 아니라면 return
  }
  const fireNotif = () => {
    if (Notification.permission !== "granted") {
      // 알림 권한 확인
      Notification.requestPermission().then((permission) => {
        // 알림을 표시할 지 요청
        if (permission === "granted") {
          new Notification(title, options);
          // 알림 표시가 허용되면 알림 반환
        } else {
          return; // 거절되면 return
        }
      });
    } else {
      new Notification(title, options);
      // 알림이 이미 허용되어 있을 경우
    }
  };
  return fireNotif;
};

const App = () => {
  const triggerNotif = useNotification("Hey", { body: "Nope" });
  return (
    <div className="App">
      <button onClick={triggerNotif}>Hello</button>
    </div>
  );
};
```

- 알림을 실행하는 함수형 프로그래밍

#### 코드실행결과

<img src="../images/notification.png" alt="useNotification"></img>
