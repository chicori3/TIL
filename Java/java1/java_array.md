## 배열

```java
int score1, score2, score3, score4;

int[] score = new int[4]; // 배열
```
**같은 타입의 여러 변수를 하나의 묶음으로 다루는 것**   

### 배열의 선언과 초기화

```java
// 배열의 선언
int[] score;
String[] name;

// 초기화
int[] arr = new int[3]; // 선언과 동시에 초기화 가능
int[] arr2 = new int[]{1, 2, 3}; // 선언과 동시에 초기화 가능
int[] arr3 = {1, 2, 3}; // 이미 선언된 배열도 이 방법으로 초기화
```

배열을 다루기 위한 **참조변수의 선언**

### 배열의 인덱스

각 요소에 자동으로 붙는 번호   
인덱스의 범위는 **0부터 '배열길이 - 1'까지**

### 배열 기본값

배열은 따로 값을 입력하지 않으면 각 데이터 타입에 따른 기본값을 가진다

|배열의 타입|기본값
|:-:|:-:
|char|'u\0000'
|byte, short, int|0
|long|0L
|float|0.0F
|double|0.0, 0.0D
|boolean|false
|배열, 인스턴스 등|null
