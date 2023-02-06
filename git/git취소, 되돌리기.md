## git clean
- Git에서 추적하지 않는 파일들 삭제

```
-n: 삭제될 파일들 보여주기
-i: 인터렉티브 모드 시작
-d: 폴더 포함
-f: 강제로 바로 지워버리기
-x: .gitignore에 등록된 파일들도 삭제
```

## git restore
- 특정 파일을 지정된 상태로 복구

- git restore (파일명): 워킹 디렉토리의 특정 파일 복구 (git restore .은 모든 파일 복구)

- git restore --staged (파일명): 스테이지에서 워킹 디렉토리로 돌려놓기

- git restore --source=(헤드 또는 커밋 해시) (파일명): 특정 커밋의 상태로 되돌리기


## git reflog
- reset으로 사라진 커밋을 복구할 수 있는 명령어

- reflog는 프로젝트가 위치한 커밋이 바뀔 때마다 기록되는 내역을 보여주고 이를 사용하여 reset하기 이전 시점으로 프로젝트를 복구할 수 있다.