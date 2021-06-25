# 구조체

## 구조체란?

1. 사용자 정의 데이터 타입
2. 관련 있는 데이터를 묶어서 처리할 수 있는 자료 구조
3. 서로 다른 데이터 타입을 묶어 사용자가 정의하는 데이터 타입
    > 배열은 서로 같은 데이터 타입의 묶음

## 구조체 정의 방법

1. 구조체의 멤버로 일반 변수, 배열, 포인터 선언 가능
2. 구조체를 정의하면 새로운 데이터 타입이 만들어짐
3. 구조체 정의 -> 메모리 할당의 의미는 아님
4. 구조체형 변수 선언 -> 메모리 할당
5. 구조체의 크기는 모든 멤버들의 크기의 합보다 크거나 같음
6. 구조체 멤버 중 가장 큰 멤버의 크기를 기준으로 멤버 할당(padding)
7. 구조체의 크기를 구하려면 `sizeof 연산자`를 이용함

```c++
// 구조체 구조
struct student {
    char name[20];
    int num, kor, eng, mat;
    double average;
};
```
## 구조체 선언

1. 구조체 변수를 선언하면 구조체 변수가 가진 멤버들이 메모리에 선언된 순서대로 할당됨
2. 구조체를 정의하면서 구조체 변수를 함께 선언할 수 있음

```c++
struct point {
    int x;
    int y;
} p1, p2;
```
3. 구조체를 정의하면서 변수를 함께 선언할 때는 태그명을 생략 가능

```c++
struct {
    char sex;
    int age;
} m1, m2;
```

## 구조체 처리

1. 선언 시 초기화는 배열 초기화와 동일
2. {} 안에 멤버들의 초기값을 순서대로 나열
3. {} 안에 지정한 초기값이 멤버의 개수보다 부족하면 나머지 멤버들은 0으로 초기화
4. 멤버 접근 연산자 `.`를 이용한 초기화 가능
5. 같은 구조체형의 변수끼리는 서로 초기화나 대입 가능
6. 구조체 간의 초기화 : 멤버 대 멤버 초기화
7. 구조체 간의 대입 : 멤버 대 멤버 대입

## 구조체 응용

### 1. 구조체 멤버

구조체 멤버를 다른 구조체 멤버로 사용 가능

```c++
struct student {
    char *name;
    int num;
    int age;
};

struct sungjuk {
    struct student stud;
    int kor, eng;
    double avg;
};
struct sungjuk m2 = { {“hong kildong”, 20200001, 27}, 95,87};
printf(“ 학번 : %d”, m2.stud.num);
```

### 2.구조체 배열

구조체를 배열로 선언 가능   
구조체 배열을 초기화하려면 {} 안에 배열 원소 초기값을 나열

```c++
struct sungjuk {
    char name[20];
    int kor, eng;
    double avg;
};
struct sungjuk m[50];

struct sungjuk m[3] = { { “hong”,95,87}, { “park”, 85, 67}, { “kim”, 78, 92} };
```

### 3. 구조체 포인터

구조체 포인터를 선언 가능   
구조체 포인터로 구조체 멤버에 접근할 때 `->` 간접 접근 연산자 사용

```c++
struct sungjuk {
    char name[20];
    int kor, eng;
    double avg;
};

struct sungjuk m2={ “hong”, 95, 87 };
struct sungjuk *ps = &m2;
m2.kor = 92;
ps -> kor = 92;
```