## 태그
- 특정 시점을 키워드로 저장하고 싶을 때

- 커밋에 버전 정보를 붙이고자 할 때

### 태그 종류
- lightweight: 특정 커밋을 가리키는 용도

- annotated: 작성자 정보와 날짜, 메시지, GPG 서명 포함 기능

### 마지막 커밋에 태그 달기 (lightweight)
- git tag v2.0.0

### 현존하는 태그 확인
- git tag

### 원하는 태그 내용 확인
- git show v2.0.0

### 태그 삭제
git tag -d v2.0.0

### 마지막 커밋에 태그 달기 (annotated)
- git tag -a v2.0.0

- git tag v2.0.0 -m "tag message"
  . -m 태그가 -a태그 암시
  . git show v2.0.0으로 확인

### 원하는 커밋에 태그 달기
- git tag (태그명) (커밋 해시) -m (메시지)

### 원하는 패턴으로 필터링하기
- git tag -l "패턴*"

### 원하는 버전으로 체크아웃
- git checkout (태그명)


## 원격 태그 관리

- git push (원격명) (태그명): 특정 태그 원격에 push

- git push --delete (원격명) (태그명): 특정 태그 원격에서 삭제

- git push --tags: 모든 태그 원격에 push

### git release

- 릴리즈 버전 표시 깃허브에서 tag -> create release