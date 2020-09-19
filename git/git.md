# Git

> [참조링크](https://rogerdudler.github.io/git-guide/index.ko.html)

- 분산형 버전 관리 시스템.
- 오프라인 작업이 가능하며 빠르다.

## Git 사용법

1. Git 저장소 만들기

```
git init
```

1. Git 저장소 받아오기

```
git clone /로컬/저장소/경로
git clone 사용자명@호스트:/원격/저장소/경로
```

1. Git 원격 서버 연동

```
git remote add origin 원격 서버 주소
```

1. Commit 하기

```
git add .
git commit -m "설명"
```

1. Push 하기

```
git push origin master
```

1. Branch 이용
   > master branch를 해치지 않고 작업할 때 사용

```js
// 가지 생성
git checkout -b 가지 이름

// master 가지로 돌아오기
git checkout master

// 가지 삭제
git branch -d 가지 이름

// 가지 push
git push origin 가지 이름
```

1. 갱신과 병합

```js
// 로컬 저장소와 원격 저장소 병합
git pull

// 다른 가지의 변경 내용을 현재 가지에 병합하기
git merge 가지 이름
git add 파일 이름

// 변경 내용 비교
git diff 원래 가지 비교 대상 가지
```

1. 로컬 변경 내용 되돌리기

```js
git checkout -- 파일 이름

// 로컬의 변경 내용 대신 원격 저장소의 최신 이력 가져오기
git fetch origin
git reset --hard origin/master
```
