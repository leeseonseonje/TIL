## git diff
- 워킹 디렉토리의 변경사항 확인

- git diff --name-only: 워킹디렉토리 변경사항 파일 이름만 확인

## git diff --staged
- 스테이징되어있는 변경사항 확인

- git diff --staged --name-only: 이름만

- git cached도 가능 (같은 기능)

## git diff (커밋1) (커밋2)
- 커밋 해시 또는 HEAD 번호로 입력

- 현재 커밋과 비교하려면 이전 커밋만 명시

- git diff --name-only (commit) (commit)

## git diff (브랜치1) (브랜치2)

- 브랜치 비교

- git diff --name-only (branch) (branch)

## git blame (파일명)
- 파일의 부분별로 작성자 확인하기

## git bisect
- 이진 탐색으로 문제 발생 시점 찾아냄

- git bisect start: 이진 탐색 시작

- git bisect bad: 오류발생 지정임을 표시

- git bisect good: 오류 없으면 정상 표시

- git bisect reset: 이진 탐색 종료