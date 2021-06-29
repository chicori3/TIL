# 공용체와 열거체

## 1. 공용체 활용

공용체 : 동일한 저장 장소에 여러 데이터 타입을 저장하는 자료 구조

1. 멤버들이 **메모리를 공유해서 사용**하는 기법
2. 공용체의 크기는 공용체의 멤버 중 **가장 큰 멤버에 의해 결정**
3. 공용체 변수를 초기화할 때는 첫 번째 멤버의 초기값만 지정
4. 공용체의 멤버에 접근할 때도 `.`와 `->` 연산자를 사용

## 2. 비트필드

1. 구조체가 가진 멤버를 **비트 단위**로 사용
2. 비트필드 정의

```c++
struct Date {
    int day:5; // 1~31
    int month:4; // 1~12
    int year:13; // 1~4096
};
```
3. 메모리에 할당할 때, **첫 번째 멤버를 최하위 비트에서부터 할당**

4. 비트필드의 멤버에 표현 가능한 범위 밖의 값을 지정하면 오버플로우 발생

```c++
#include <stdio.h>
struct Date {
    int day:5; // 1~31
    int month:4; // 1~12
    int year:13; // 1~4096
};
int main()
{
    struct Date ent;
    ent.month = 17;
    printf("%d \n", ent.month);
    printf("size %d", sizeof(ent));
    return 0;
}
```

5. 비트필드를 정의할 때는 중간에 일부 비트를 비워두고 멤버를 특정 비트에 할당할 수 있음

> 리틀 엔디안 : 최하위 바이트부터 메모리에 저장하는 방식
> 빅 엔디안 : 최상위 바이트부터 메모리에 저장하는 방식

## 3. 열거체 활용

1. 나열된 정수 값 중 하나를 갖는 정수형의 일종

```c++
enum week { sun, mon, tue, wed, thu, fri, sat };    // sun = 0, mon = 1 로 정의됨
enum color { red = 10, green = 20, blue = 30 };     // red = 10, green = 20 으로 정의됨
```

2. 일종의 사용자 정의형
3. 열거체 변수에는 열거체 정의에 나열된 열거 상수 중 하나를 저장하고 사용
4. 열거 상수만 정수형 상수로 정의할 수도 있음
5. 프로그램의 가독성을 향상시키기 위해 사용

## 4. typedf

1. 데이터 타입의 이름을 **새로운 이름**으로 재정의
2. 코딩의 편리성 증대
3. 프로그램의 시스템 간 호환성 향상
