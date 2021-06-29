# 파이썬의 파일 입출력

## 파일 입출력이란

파일을 열어 자료를 읽거나, 쓰거나, 수정한 후 파일을 닫는 작업   

`open > 읽기, 쓰기, 수정 > close()`

파일 처리 후 `close()`를 통해 닫아주어야만 자원 점유를 해제하고 불필요한 오류 발생을 막을 수 있음

|모드|의미|비고
|:-:|:-:|:-
|r|읽기 모드|파일 객체를 읽기모드로 생성<br> 파일의 처음 위치로 포인터를 이동
|w|쓰기 모드|파일을 쓰기 모드로 엶<br>파일에 데이터를 쓰면 기존 파일의 내용은 모두 사라짐<br>주어진 파일이 존재하지 않으면 새로운 파일 생성
|x|쓰기 전용|새 파일 쓰기 모드로 엶<br>주어진 이름의 파일이 존재하면 에러 발생
|a|추가 모드|파일을 추가 모드로 엶<br>기존 파일의 내용의 끝에 새 내용을 추가
|+|갱신 모드|파일을 읽기와 쓰기가 모두 가능한 모드로 엶

## 파일 쓰기

1. 파일명으로 파일을 생성 후 `write()` 함수를 활용해 내용 작성 가능
    > 디렉터리 경로 없이 파일명만 적은 경우 현재 해당 파이썬이 실행되는 경로에 생성

```py
f = open("a.txt",'w')
f.write("1234")
f.close
```

2. 특정 경로에 파일을 생성하고 싶을 때는 **전체 경로 및 파일명 입력**
    > \는 이스케이프 문자로 경로 설정 시 주의

```py
f = open("C:\\Users\\...\\a.txt",'w')
```

3. w 모드일 경우 파일을 새로 생성하며, 기존에 파일이 있다면 덮어씀
4. 기존 파일에 새로운 내용을 추가하려면 a 모드 사용
5. 새로운 파일을 쓰기 위해 x 모드도 사용 가능
    > w 모드와 기능은 똑같지만, x 모드는 기존 파일이 있다면 오류 발생 (덮어쓰기 방지)

6. 여러 줄의 내용을 입력하는 방법
    > 여러 줄 문자열 사용 (따옴표 세 개)
    > 개행 문자 사용

```py
f = open("a.txt",'w')
f.write(""""1234
1234"""")
f.write("1234\n1234")
f.close()
```

7. 리스트, 튜플 등의 내용을 입력하는 방법
    > `writelines()` 함수 사용

```py
t = ("1","2")
l = ["1","2"]
f = open("a.txt",'w')
f.writelines(t)
f.writelines(l)
f.close()
```

8. r 모드로 파일 열기, `read()` 함수로 파일 전체 내용 불러오기
    > 읽으려는 파일이 없으면 오류 발생

9. `readline()` 함수로 파일의 내용을 한 줄씩 가져올 수 있음
    > 더 이상 읽을 줄이 없다면 `None()`을 반환
    > while + if 제어문을 사용하여 모든 줄 출력 가능

```py
f = open("a.txt",'r')
while True:
    line = f.readline()
    if not line:
        break
    print(line)
f.close()
```

10. `readlines()` 함수로 파일의 내용을 리스트로 가져올 수 있음
    > 주로 반복문과 함께 사용해 한 줄씩 리스트의 요소로 가져와 활용

```py
f = open("a.txt",'r')
print(f.readlines())
f.close()
```

## 표준 출력 전환

파이썬의 표준 출력은 `print()` 함수를 활용해 파이썬 쉘 환경(콘솔)에 출력
> 파이썬의 sys 모듈을 활용해 표준 출력을 파일로 전환 가능
> 표준 입출력 : 프로그램 내에서 특정 장치를 지정하지 않아도 시스템이 default로 사용하는 장치에 입출력하는 것

- `sys.stdout` : 표준 출력
- `sys.stdin` : 표준 입력

```py
import sys
f = open('a.txt','w')
sys.stdout = f
print("1234")
f.close()
```

1. **로그, 에러 등을 기록**할 때 활용 가능
    > 표준 출력을 잠시 다른 변수에 저장해두고 필요할 때 콘솔로 되돌려서 사용

```py
import sys
stdout = sys.stdout
sys.stdout = 파일

sys.stdout = stdout
```

2. 기존 파일 입출력은 단순 텍스트만 파일로 입출력 가능
    > 다른 자료형의 객체의 형태를 그대로 유지하면서 파일에 저장하기 위해 pickle 모듈 활용

```py
f = open("a.txt",'w')
f.write("[1,2,3]")
f.close()
f = open("a.txt",'r')
a = f.read()
f.close()
print(a)                # [1,2,3]
print(type(a))          # <class 'str'>
```

3. pickle 모듈로 파일을 저장할 때는 **바이너리 형식**으로 입출력해야 함 (wb, rb 모드)
    > 파이썬의 모든 객체들을 그대로 저장 가능

```py
import pickle
f = open("a.txt",'wb')
data = {1: 'pyton', 2: 'god'}
pickle.dump(data, f)            # 깨진 글자가 저장됨
f.close()

f = open("a.txt",'rb')
data_read = pickle.load(f)
f.close()
print(data_read)                # {1: 'pyton', 2: 'god'}
print(type(data_read))          # <class 'dict'>
```

## 파일 다루기

시스템의 환경 변수, 디렉터리, 파일 등을 제어할 수 있는 파이썬의 OS 모듈 활용

1. `listdir()` 함수로 해당 디렉터리의 파일 목록 반환

```py
print(os.listdir('.'))
# .은 현재 디렉터리 ../은 부모 디렉터리
```

2. `rename()` 함수로 파일의 이름 변경

```py
os.rename('a.txt','b.txt')
```

3. `path.exists()` 함수로 파일의 존재 유무 확인

```py
path.exists('a.txt')    # False
path.exists('b.txt')    # True
```

4. `path.abspath()` 함수로 파일의 존재 유무와 관계없이 해당 파일의 절대 경로 반환
    > 파일이 없어도 생성 가능하므로, 파일을 입력할 때 자주 활용

```py
print(os.path.exists('a.txt'))  # False지만 절대 경로 반환
print(os.path.exists('b.txt'))  # True
```

5. `path.basename()`, `dirname()`, `split()` 함수로 해당 파일의 파일명과 경로명을 분리, 반환
    > 파일명과 파일의 경로명을 따로 분리 가능
    > 환경마다 위치가 다를 경우 자주 활용

6. `path.splitdrive()`, `splitext()` 함수로 해당 파일 경로의 드라이브, 확장자를 분리, 반환
    > 저장된 드라이브가 다르거나, doc, docx 처럼 확장자가 다를 경우 자주 활용

## 디렉터리 다루기

1. `getcwd()` 함수로 현재 작업 중인 디렉터리 반환
    > cwd : Current Working Directory

```py
print(os.getcwd())          # C:\\헌 폴더
```

2. `chdir()` 함수로 현재 작업 중인 디렉터리 경로 변경
    > chdir : Change Directory

```py
os.chdir('C:\\새 폴더')     # C:\\새 폴더
```

3. `mkdir()` 함수로 새 폴더 생성
    > mkdir : Make Directory

```py
os.mkdir('temp')
```