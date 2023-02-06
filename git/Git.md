## reset, revert

- reset: 과거로 돌아감, 현재기록 남지 않음
- revert: 현재의 이력을 남기고 과거로 돌아감, 새로운 commit을 생성하면서 과거로 돌아감

## merge, rebase

- merge: 두 개의 branch를 이어 붙히는 것 이 과정으로 커밋 하나가 생겨나게 된다.
  ![](https://velog.velcdn.com/images/leeseonseonje/post/9b6c2f5c-894b-4629-9805-17d3b46c0984/image.png)

- rebase: 브랜치의 마디, 커밋들을 대상 	브랜치로 옮겨 붙이는 것
  ![](https://velog.velcdn.com/images/leeseonseonje/post/0af25ce4-9272-4d22-a8e8-466b363fdea3/image.png)

### 차이?
rebase를 한 뒤 히스토리는 한 줄로 깔끔하게 정리되지만, merge는 브랜치에 흔적을 남긴다.
많은 브랜치를 사용하는 프로젝트에서는 merge는 굉장히 복잡해진다.

- merge는 브랜치들을 놔두고 끝에만 모아서 병합하기 때문에 잔가지들이 남지만, rebase는 가지들을 잘라 몸통 줄기에다 이어 붙이는거기 때문에 히스토리를 깔끔하게 한 줄로 유지할 수 있다.

## Git의 세가지 공간
- Working directory: 새로운 파일이 추가되거나, 기존 파일이 변경, 삭제된 경우
    - untracked: Add된 적 없는 파일, ignore된 파일
    - tracked: Add된 적 있고, 변경내역이 있는 파일

- Staging area: Working directory의 파일들을 add하게 되면 Staging area에 들어가게 된다.

- Repository: Staging area의 파일들을 commit하게 되면 Repository에 들어가게 된다.

### git rm
- 파일 삭제 하면 파일의 삭제내역이 working directory에 있다.

- 파일의 삭제를 git rm 명령어로 하게 되면, 파일의 삭제내역이 staging area에 있다.

### git mv
- 파일의 이름을 변경하게 되면, working directory의 변경하기 전 파일의 삭제가 tracked영역에 있게되고 변경한 파일의 생성이 untracked에 있게된다. 이 후 add를 해야 파일의 이름이 바뀐거라고 git이 인식한다.

- 파일의 이름 변경을 git mv명령어로 하게 되면 바로 파일의 이름 변경을 git이 인식한다.
  (add된 상태 즉, staging area에 있는 상태)

#### git restore --staged (파일명)
- staging area에 있는 파일을 working directory로 되돌리는 명령어

#### git reset 세 가지 옵션
- soft: repository에서만 제거하고, staging area에 남겨 놓는다.
  (add는 하고 commit은 되지않는 상태)

- mixed: 어떠한 변화를 working direectory에 남겨 놓는다. staging area에서 지운다.

- hard: 내역 자체를 지운다. 즉, 어떠한 변화를 working directory까지 삭제한다.

## HEAD
- 현재 속한 브랜치의 가장 최신 커밋

### git checkout HEAD^
- ^또는 ~의 개수만큼 이전으로 이동

- 커밋 내역 그대로 남겨두고 파일들의 상태만 이동함

### git checkout ~
- 한 단계 되돌리기

#### 커밋 해시로도 체크아웃이 가능하다. ex)git checkout fjqe343

### HEAD Branch
- HEAD로 이동하게 되면 익명의 다른 브랜치가 만들어져 있게된다.

## git config
- --global: 전역 설정

- --global 빼고하면 현재 깃만 설정

- --wait: 에디터에서 수정하는동안 CLI 금지

git config --global core.editor /usr/bin/vim

- git config --global core.autocrlf (window: true / mac: input)
    - 줄바꿈 호환 문제 해결

- git config --global init.defaultBranch main
    - 기본 브랜치명 (master -> main으로 변경)

- git config --global push.default current
    - push시 로컬과 동일한 브랜치명으로

-  git config --global alias.(단축키) "명령어"
    - 별칭 지정
    - ex) git config --global alias.cam "commit -am"