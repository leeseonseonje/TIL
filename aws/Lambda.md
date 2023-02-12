<!-- @format -->

# Lambda

-   Serverless의 구축을 담당

    -   Serverless? cloud가 직접 서버를 관리하며 resource를 서버의 사용량에 따라 직접 할당해준다.

-   Events를 통하여 Lambda를 실행시킨다.

-   Lambda Function

## 비용

-   Lambda Funciton이 실행될때만 돈이 지붋된다.

-   매달 백만번 함수 호출은 무료(그 후로 유료)

## Tip

-   최대 5분 런타임 시간 허용 (이 이상 늘리는 것은 불가능하다)
-   512MB의 일시적인 디스크 공간 제공(/tmp/)
-   최대 50MB Deployment Package 허용(로컬 에서 작성한 파일을 AWS에 업로드해서 디플로이할 수 있다.)
    -   용량이 초과 될 경우 S3 버켓에 업로드

## 예시

1. S3 -> put object

2. put object이벤트가 lambda function 실행

3. lambda가 데이터 변환, 불필요한 데이터 삭제

4. DB에 깨끗한 데이터를 업로드 시킨다.

## 예시2

1. Topic으로 데이터를 보낸다.

2. lambda function 실행

3. lambda가 데이터 변환

4. SNS을 통하여 사용자에게 실시간으로 알려줌
