# 조건문

조건을 판단해서 참인 경우 문장 수행

## if문

```c
if(조건)
실행문;
```

- 조건에 따라 분기되는 if문은 크게 3가지 형태로 구분됨
- if문 내에 중첩해서 if문을 기술하는 것이 가능함
- 조건에 따라 수행하는 문장이 한 문장이면 { }는 생략 가능함

1. if

```c
int a = 5;
if(a>0)
    printf("Positive.\n");
```

**if**의 조건이 참일 경우 아래 문장을 실행하게 된다



2. if ~ else

```c
int a = 5;
if(a>0)
    printf("Positive"); // true
else
    printf("Negative"); // false
```

**if**문의 조건이 거짓일 경우 **else**의 문장을 실행하게 된다

3. if ~ else if ~ else

```c
int a=5;
if(a>0)
    printf("Positive");
else if(a<0)
    printf("Negative");
else
    printf("Zero");
```

조건이 3가지 이상일 때 사용하며 `else if`는 여러 번 사용할 수 있다.

## switch문

```c
switch( 값 )
{
    case 값1 : 문장1-1; 문장1-2; break;
    case 값2 : 문장2-1; 문장2-2; break;
    case 값3 : 문장3-1; 문장3-2; break;
    . . .
    default : 문장d1; 문장d2;
}
```
- switch문에서 분기 조건으로 상수, 정수, 수식이 사용될 수 있음
- 조건에 일치하는 case가 없는 경우 수행할 문장은 default에
기술함
- 표준입력 함수로 scanf()를 사용하고 입력을 위해 형식지정자를
사용함
- 입력 버퍼를 비우는 함수로 fflush(stdin);함수가 있음

```c
int a=2;
switch(a)
{
    case 1 : printf(“one”); break;
    case 2 : printf(“two”); break;
    case 3 : printf(“three”); break;
    default : printf(“other”);
}
```
### 입력문

#### scanf()

- `scanf()`를 이용한 입력
- 표준 입력으로부터 다양한 자료를 지정한 변수에 저장
- 형식지정자 사용
- 공백, enter 전까지 입력
- 형식 : `scanf("형식지정자",&변수명)`

정수 입력 : %d
실수 입력 : %f, %lf
문자 입력 : %c