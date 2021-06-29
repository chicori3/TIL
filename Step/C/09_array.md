# 배열

- 동일한 이름으로 참조되는 연속된 메모리에 할당된 자료 구조
- **같은 데이터 타입을 묶어 하나의 공간처럼 사용**할 수 있음

## 배열 이해

### 특징
- 많은 수의 변수 이름을 생성할 필요가 없음
- 동일한 이름을 사용하므로 반복문
- 요소 : 배열을 구성하는 항목
- 크기 : 배열 요소의 개수
    - 양의 정수, 매크로 상수, 관련 연산식으로 지정
    - 변수, const 상수 불가
- 첨자 : 각 요소에 부여되는 위치 정보

```c
// 가능
#define SIZE 5

int a[100];
double b[20];
int c[SIZE];
char d[SIZE+1];

// 불가능
int size=5;

int a[100];
double b[20];
int c[size];
char d[size+1];
float e[3.5];
int f[-3];
short g[0];
```

### 참조

- 각 요소에 대한 참조는 `index` 이용
- 0 ~ size-1
- 배열명[index]
- 범위 밖의 요소를 참조하는 경우 에러 발생

### 초기화

- 각 요소는 순서대로 `index 0`부터 초기화
- 배열 크기보다 초기화 요소수가 적으면 나머지는 0
- 초기화하지 않은 지역 배열 요소는 쓰레기 값을 가짐
- 선언과 초기화를 같이 하는 경우 크기 생략 가능

```c
int a[4]={1,2,3};   // 1, 2, 3, 0
int a[]={1,2,3};    // 1, 2, 3
int a[3]={0};       // 0, 0, 0
```

```c
// 50명의 성적을 출력하고 학급평균 처리하기
#include <stdio.h>

int main()
{
    int I, kor[50], sum=0;
    for( i=0 ; i<50 ; i++ )
    {
        printf(“%d번 학생의 국어점수를 입력하세요 ”);
        scanf(“%d”, &kor[i] );
        sum += kor[i]
    }
    for( i=0 ; i<50 ; i++ )
    {
        printf(“%d번 학생의 국어점수 : %d \n“, kor[i] );
    }
    printf(“학급평균은 %f 이다”, sum/50.0);
    return 0;
}
```

변수를 50개 만드는 것보다 효율적으로 코드를 작성할 수 있다

## 다차원 배열

- 필요 시 2차원 이상의 배열 형태를 구현할 수 있다
- 실제 메모리 구조는 인접한 메모리의 연속
- 초기값을 생략하면 나머지 원소를 0으로 초기화
- 행 크기는 생략 가능, 열 크기는 생략 불가