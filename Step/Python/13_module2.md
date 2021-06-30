# 파이썬 외부 모듈의 활용

## 외부 모듈이란

다른 사람이 개발한 소프트웨어를 사용 가능
> 파이썬 패키지 인덱스 PyPI 라이브러리 저장소 관리 기구가 있음  

4차 산업혁명 관련 IT 분야에서 파이썬의 중요성이 높아진 이유
> 외부 모듈을 다양하게 제공하기 때문

## 외부 모듈 설치하기

1. 패키지 관리자 PIP 사용하기

2. `pip install 패키지명`
3. Jupyter Notebook 환경에서 명령어 앞 `!`를 붙여 설치 가능
    > !를 붙이면 콘솔창에 입력하는 것과 같은 역할
    > pip uninstall 모듈명
4. 일반 사용자들이 개발한 모듈도 사용 가능

## 데이터베이스 연결하기

pymysql : MySQL을 파이썬에서 사용할 수 있는 모듈

- `pip install pymysql`
- MySQL 설치
    > 오픈 소스 관계형 데이터베이스

1. 데이터베이스 서버 환경
    - test db에 test 테이블 생성

```sql
-- 스키마 생성 코드
CREATE DATABASE `test` /*!40100 DEFAULT CHARACTER SET 
latin1 */;

-- 테이블 생성 코드
CREATE TABLE `test` (
`id` int(11) NOT NULL AUTO_INCREMENT,
`name` varchar(500) CHARACTER SET utf8 DEFAULT NULL,
`age` int(11) DEFAULT NULL,
`enable` varchar(45) DEFAULT '0',
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```

2. 모듈 import, 연결 정보 정의
    > 서버 주소, 포트번호, 아이디, 비밀번호
3. 데이터 가져오기
4. 데이터 입력하기

## 웹 크롤링하기

웹 사이트에서 원하는 정보를 추출하는 것

- 웹 크롤링 대표 라이브러리 BeautifulSoulp 설치

- `pip install beautifulsoup4`

1. urllib 모듈로 웹 페이지 가져오기
    > 파이썬에서 웹과 관련된 작업을 도와주는 모듈

2. BeautifulSoup 모듈로 웹 페이지 분석
3. 급상승 검색어 부분의 패턴 찾기
4. 찾은 패턴으로 내용 추출
5. 필요한 정보만 가공하여 마무리