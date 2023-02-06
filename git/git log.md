## git log -p
- 각 커밋마다 변경사항 함께 보기

## git log -(갯수)
- 최근 n개 커밋만 보기


## git log --stat
- 통계
- git log --shortstat: 통계 짧게

## git log --oneline
- 로그 한줄로 보기

## git log -S (검색어)
- 변경사항 내 단어 검색

## git log -grep (검색어)
- 커밋 메시지로 로그 검색


git log --graph --all --pretty=format:'%C(yellow) %h  %C(reset)%C(blue)%ad%C(reset) : %C(white)%s %C(bold green)-- %an%C(reset) %C(bold red)%d%C(reset)' --date=short