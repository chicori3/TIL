## 배열

```java
int score1, score2, score3, score4;

int[] score = new int[4]; // 배열
```
**같은 타입의 여러 변수를 하나의 묶음으로 다루는 것**   

### 선언과 초기화

```java
// 배열의 선언
int[] score;
String[] name;

// 초기화
int[] arr = new int[3]; // 선언과 동시에 초기화 가능
int[] arr2 = new int[]{1, 2, 3}; // 선언과 동시에 초기화 가능
int[] arr3 = {1, 2, 3}; // 이미 선언된 배열도 이 방법으로 초기화
arr[1] = 20; // 인덱스에 직접 초기화 가능
```

배열을 다루기 위한 **참조변수의 선언**

### 인덱스

각 요소에 자동으로 붙는 번호   
인덱스의 범위는 **0부터 '배열길이 - 1'까지**

### 기본값

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

### 길이

```java
배열이름.length - 배열의 길이(int형 상수)
int[] arr = new int[5]; // 길이가 5인 배열
int tmp = arr.length; // arr.length의 값은 5이고 tmp에 저장
```

**배열은 한 번 생성하면 길이를 바꿀 수 없음**   
대신 새로운 배열에 기존의 배열의 요소들을 복사하여 크기를 조정할 수는 있다

### 출력

```java
int[] iArr = {100, 95, 80};
char[] chArr = {'a', 'b', 'c'};

System.out.println(iArr); // iArr의 주소 I@...가 출력된다
System.out.println(chArr); // 문자 배열은 'a', 'b', 'c' 가 출력된다

// 배열의 모든 요소 출력
int[] score = new int[5];

for (int i = 0; i < score.length; i++) { // for문 이용
	System.out.println(score[i]);
}

System.out.println(Arrays.toString(iArr); // Arrays.toString() 이용
```

### 활용

```java
// 총합과 평균
int sum = 0; // 총합을 저장하는 변수
float average = 0f; // 평균을 저장하는 변수

int[] score = { 100, 80, 100, 77, 65 };

for (int i = 0; i < score.length; i++) {
	sum += score[i]; // 반복해서 배열의 값을 더한다
}

average = sum / (float) score.length; // 계산 결과를 float타입으로 형변환

System.out.println("총합 " + sum);
System.out.println("평균 " + average);

// 최대값과 최소값
int[] score = { 100, 80, 100, 77, 65 };

int max = score[0]; // 최대값을 저장하는 변수
int min = score[0]; // 최소값을 저장하는 변수

for (int i = 1; i < score.length; i++) {
	if (score[i] > max) { // i가 max보다 크면
		max = score[i]; // i를 max에 할당
	} else if (score[i] < min) { // i가 min보다 작으면
		min = score[i]; // i를 min에 할당
	}
}

System.out.println("최대값 " + max);
System.out.println("최소값 " + min);

// 섞기
int[] numArr = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
System.out.println(Arrays.toString(numArr));

for (int i = 0; i < 100; i++) {
	int n = (int) (Math.random() * 10); // 0~9 중 하나를 임의로 얻는다

	// i와 n의 값을 서로 바꾼다
	int tmp = numArr[i];
	numArr[i] = numArr[n];
	numArr[n] = tmp;
}

System.out.println(Arrays.toString(numArr));

// 로또
int[] ball = new int[45]; // 45개의 정수값을 저장하는 배열

// 배열의 각 요소에 1~45의 값을 저장
for (int i = 0; i < ball.length; i++)
	ball[i] = i + 1; // ball[0]에 1이 저장된다

int tmp = 0; // 두 값을 바꿀 때 쓸 임시변수
int j = 0; // 임의의 값을 저장할 변수

// 배열의 i번째 요소와 임의의 요소에 저장된 값을 서로 바꿔 섞는다
// 0번째부터 5번째 요소까지 모두 6개만 바꾼다
for (int i = 0; i < 6; i++) {
	j = (int) (Math.random() * 45); // 0~44 범위의 임의 값
	tmp = ball[i];
	ball[i] = ball[j];
	ball[j] = tmp;
}

// 배열 ball의 앞에서부터 6개의 요소를 출력한다
for (int i = 0; i < 6; i++) {
	System.out.printf("ball[%d]=%d\n", i, ball[i]);
}
```

### 다차원 배열

#### 2차원 배열
```java
// 선언
int[][] score = new int[4][3]; // 4행 3열의 2차원 배열

// 초기화
int[][] arr = { { 1, 2, 3 }, { 4, 5, 6 } };

// 인덱스
score[1][2]; // 2행 3열의 인덱스
```

**1차원 배열의 배열**
테이블 형태의 데이터를 저장하기 위한 배열   

### Arrays로 배열 다루기

```java
// 배열의 출력
int[] arr = {0, 1, 2, 3};
int[][] arr2d = {{11, 12}, {21, 22}};

System.out.println(Arrays.toString(arr)); // [0, 1, 2, 3]
System.out.println(Arrays.deepToString(arr2d)); // [[11, 12], [21, 22]]

// 배열의 비교
String[][] str2d = new String[][] { { "aa", "bb" }, { "AA", "BB" } };
String[][] str2d2 = new String[][] { { "aa", "bb" }, { "AA", "BB" } };
		
System.out.println(Arrays.equals(str2d, str2d2)); // false
System.out.println(Arrays.deepEquals(str2d, str2d2)); // true

// 배열의 복사
int[] arr = { 0, 1, 2, 3 };
int[] arr2 = Arrays.copyOf(arr, arr.length); // arr의 길이만큼 복사
int[] arr3 = Arrays.copyOfRange(arr, 2, 4); // arr의 index 2이상 4미만까지 복사

// 배열의 정렬
int[] arr = { 3, 2, 0, 1, 4 };
Arrays.sort(arr); // 오름차순 정렬
System.out.println(Arrays.toString(arr)); // [0, 1, 2, 3, 4]
```











