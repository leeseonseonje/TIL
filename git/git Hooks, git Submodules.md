## Git Hooks
- Git상의 이벤트마다 자동으로 실행될 스크립트를 지정합니다.

## gitmoji
- 커밋 메시지에 이모지 추가 가능

## 다운로드
- brew install gitmoji

## 초기화

- gitmoji -i

## 사용
- add후 git commit 명렁어를 입력하면 아래와같이 이모지를 선택할 수 있는 창이 뜬다.(검색 가능) 이 후 메시지를 입력 후 커밋한다.

![](https://velog.velcdn.com/images/leeseonseonje/post/c4e98771-7b7b-4d14-bc84-63477fc63b23/image.png)

- 커밋 후 푸시하면 아래사진과 같이 깃허브 커밋메시지에 이모지가 생긴다.
  ![](https://velog.velcdn.com/images/leeseonseonje/post/5b8811a5-31bf-4f99-82b0-5e48b9423939/image.png)

## 서브모듈
- 프로젝트 안에 다른 프로젝트가 포함될 때 사용

- 여러 프로젝트에 사용되는 공통모듈일때 유용하다.

- git submodulea add "github repository"

- .gitmodules파일 생성

- main프로젝트에서 add 하면 main프로젝트에 있는 파일만 스테이징된다.

- sub프로젝트를 스테이징하려면 sub프로젝트경로에서 스테이징해야한다.

- 이후 다시 main프로젝트에서 커밋 후 푸시해야한다.(서브모듈의 변경자체는 메인에서 관리하기 때문)