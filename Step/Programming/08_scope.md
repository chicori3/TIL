# 지역변수

- 변수 스코프 : 변수 참조가 가능한 유효 범위
- 함수 내에 선언된 변수
- 변수가 선언된 블록에서만 유효
- 함수 시작 시 생성, Stack에 생성
- 함수가 종료되면 변수도 소멸
- 초기화 전 쓰레기 값을 가짐
- 매개변수도 지역변수

```c
int functionTest()
{
	int temp = 5;
	temp += result;
	
	return temp;
}

int main()
{
	int result = 10;
	printf("result 결과 : %d", functionTest()); 

	return 0;
}
```
`functionTest()`에 result 변수가 선언되지 않아서 에러가 난다

# 전역변수

- 프로그램 내 전체 함수에서 유효
- 프로그램 시작 시 생성, 데이터 영역에 생성
- 프로그램 종료 시 소멸
- 함수 밖에서 선언
- 자동으로 0으로 초기화
- 전역변수는 프로그램 전체에서 참조하므로 복잡성 증대
- 모듈화의 독립성 확보 어려움
- 메모리 공간 점유
- `extern`을 선언하여 외부에서 참조 가능

```c
int global = 10;

void globalTest()
{
	global += 5;
	printf("함수에서 전역변수 : %d\n", global);
}

int main()
{
	int result = 10;
	printf("전역변수 : %d\n", global);
	printf("지역변수 : %d\n", result);

	globalTest();

	return 0;
}
```
순서대로 `전역변수 : 10`, `지역변수 : 10`, `함수에서 전역변수 : 15`로 출력된다      
전역변수는 어디서든 사용되지만 가능하면 줄이고 지역변수를 사용하는 것을 권장한다
