# 포인터 배열

## 1. 1차원 포인터 배열

주소를 저장하는 배열    

1. 포인터 배열의 각 원소로 변수의 주소 저장
2. 원소가 가리키는 변수에 접근하려면 **배열의 원소 앞에 간접 참조 연산자`*`를 사용해야 함**


```c++
int* arr[5];                    // 크기가 5인 int*형 배열 선언
```

```c++
int a = 10, b = 20, c = 30;

int* arr[5] = {&a, &b, &c};     // int 변수의 주소로 arr 배열의 원소 초기화
int i;
for( i = 0 ; i < 3 ; i++ )
    printf(“%d”, *arr[i]) ;     // arr[i]는 int*형이므로 간접 참조 연산자를 사용
```

## 2. 2차원 포인터 배열

### 포인터 배열의 각 원소에 배열의 시작 주소를 저장

```c++
int main(void)
{
    int x[3] = {1, 2, 3};
    int y[3] = {4, 5, 6};
    int z[3] = {7, 8, 9};
    int* arr[3] = {x, y, z}; 
    int i, j;
    for( i = 0 ; i < 3 ; i++ )
    {
        for( j = 0 ; j < 3 ; j++)
            printf("%d ", arr[i][j]);   // *(arr[i]+j)와 같은 의미
            printf("\n");
    }
return 0;
}
```

## 3. 구조체 포인터 배열

### 구조체 배열은 메모리를 많이 사용하므로 비효율적

```c++
typedef struct student {
    char name[20];
    int korean, english, math;
    double average;
} STUDENT;

STUDENT std[ 100 ];     // STUDENT 구조체가 100개 할당되므로 40*1000 byte가 필요
```

### 구조체는 동적 메모리에 할당하고 주소만 포인터 배열에 넣어 사용 가능

```c++
STUDENT* std[100];      // 주소만 100개 할당하므로 4*100 byte가 필요
```

### 구조체 포인터 배열의 메모리 구조

```c++
STUDENT s1;
STUDENT s2;
STUDENT s3;
STUDENT* std[3] = {&s1, &s2, &s3};

printf(“%s”, std[i] → name)
```

## 4. 2차원 배열 포인터 처리

행 단위 포인터 변수

```c++
int (*p)[5];                // 크기가 5인 int 배열을 가리키는 포인터
```

```c++
int arr[3][5] = {
    { 1, 2, 3, 4, 5 },
    { 6, 7, 8, 9, 10 },
    { 11, 12, 13, 14, 15 }
};

int (*p)[5] = &arr[0];      // p를 int 5개 짜리 배열인 arr[0]의 주소로 초기화
```

### 배열에 대한 포인터를 &arr[0] 대신 arr로 초기화할 수 있음

```c++
int (*p)[5] = arr;          // arr = &arr[0] 
```

### 배열 포인터로 2차원 배열의 원소에 접근하려면 2개의 인덱스를 사용

```c++
int i, j;
for ( i = 0 ; i < 3 ; i++ )
{
    for ( j = 0 ; j < 5 ; j++ )
        printf(“%d”, p[i][j]);      // p[i][j]는 arr[i][j]를 의미
        printf(“＼n”)
}
```