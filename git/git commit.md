### 커밋 하나당 한 단위

## 커밋 메시지 컨벤션
```
type: subject

body (optional)
...
...
...

footer (optional)
```
### 예시
```
feat: 압축파일 미리보기 기능 추가

사용자의 편의를 위해 압축을 풀기 전에
다음과 같이 압축파일 미리보기를 할 수 있도록 함
 - 마우스 오른쪽 클릭
 - 윈도우 탐색기 또는 맥 파인더의 미리보기 창

Closes #125
```

![](https://velog.velcdn.com/images/leeseonseonje/post/9ac40647-d425-4be2-aa8f-c18e8ca543c3/image.png)

### Subject

- 커밋의 작업 내용 간략히 설명
### Body
- 길게 설명할 필요가 있을 시 작성


### Footer
- Breaking Point 가 있을 때

- 특정 이슈에 대한 해결 작업일 때

## git add -p
- hunk별로 스테이징

- y한것 끼리만 스테이징

- n한건 working directory에 있음

## git commit -v

- 변경사항 확인하고 커밋

- git diff --staged를하고 커밋


## git stash
- 현재 진행중인 작업들을 다른 공간으로 치워둔다.

- apply: stash 적용

- drop: stash 삭제

- pop: stash 적용, 삭제

- branch [브랜치명]: 새 브랜치를 생성하여 pop

## 커밋 수정하기

- git commit --amend: 커밋 메시지 수정

- git commit --amend -m: 커밋 메시지 한줄로 수정\

## 과거 커밋들을 수정,삭제, 병합, 분할

- git rebase -i (대상 바로 이전 커밋)

- p, pick: 커밋 그대로 두기

- r, reword: 커밋 메시지 변경

- e, edit: 수정을 위해 정지

- d, drop: 커밋 삭제

- s, squash: 이전 커밋에 합치기
  ![](https://velog.velcdn.com/images/leeseonseonje/post/adafbd14-011b-4c4f-9c0b-97b220de730c/image.png)