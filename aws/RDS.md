<!-- @format -->

# RDS

-   Relational DB Service

-   MS-SQL, Oracle, MySQL, PostgreSQL, Aurora, MariaDB

-   Data Warehousing

    -   리포트 작성, 데이터 분석시 사용

-   OLTP

    -   규모가 작은 데이터를 불러올때 사용되는 SQL쿼리가 필요할 때 유용

-   OLAP
    -   매우 큰 데이터를 불러올때 사용, 덩치가 큰 select 쿼리가 사용된다.

## Database Back-ups

-   Automated Backups(AB)

    -   Retention Period(1-35일)안의 어떤 시간으로 돌아가게 할 수 있음

    -   AB는 그날 생성된 스냅샷과 Transaction logs(TL)을 생성한다.

    -   디폴트로 AB기능이 설정되어 있으며 백업 정보는 S3에 저장된다.

    -   AB동안(S3에 데이터를 저장하는 동안) 약간의 I/O suspension이 존재할 수 있다.

    -   AB는 RDS instance를 삭제 할 시 스냅샷이 모두 사라진다.

-   DB Snapshots(데이터베이스 스냅샷)

    -   사용자에 의해 실행된다.

    -   원본 RDS instance를 삭제해도 스냅샷은 존재한다.

-   원본 RDS instance를 가지고 새로운 데이터베이스를 복원 시 새로운 RDS instance가 생성된다.

## Multi AZ

-   Multi Availability Zones

-   원래 존재하는 RDS DB에 무언가 변화(쓰기 작업)가 생길때 다른 AZ에 똑같은 복제본이 만들어 진다.

-   AWS에 의해서 자동으로 관리가 이루어진다.

-   원본 RDS DB에 문제가 생실 시 자동으로 다른 AZ의 복제본이 사용된다.

-   재해 복구 전용

-   성능 개선을 위해서 사용되지 않는다.

## Read Replicas

-   프로덕션 DB의 읽기 전용 복제본이 생성된다.

-   Read-Heavy 작업 시 효율성의 극대화를 위해 사용된다. (Scaling)

-   재해 복구 용도가 아니다.

-   최대 5개 Read Replica DB 허용

-   Read Replica의 Read Replica를 생성 가능하다.

-   각각의 Read Replica는 자기만의 고유 Endpoint가 존재한다.
    -   RDS는 IP가 아닌 Endpoint로 식별한다.

## ElasticCache

-   클라우드 내에서 in-memory 캐시를 만들어 준다.

-   DB에서 데이터를 읽어오는 것이 아니라 캐시에서 빠른 속도로 데이터를 읽어온다.

-   Read-Heavy 서비스에서 상당한 지연 감소 효과를 누린다.

-   Memcached

    -   Object 캐시 시스템이다.

    -   Elastic Cache는 Memcached의 프로토콜을 디폴트로 따른다.

    -   EC2 Auto Scaling처럼 크기가 커졌다 작아졌다가 가능하다.

    -   단순한 캐싱 모델이 필요할 경우, obejct caching, auto scaling을 원할 경우 사용한다.

-   Redis

    -   key-value, set, list와 같은 형태의 데이터를 in-memory에 저장 가능하다.

    -   Multi-AZ를 지원한다.

    -   set, list와 같은 데이터셋을 사용할 경우, 데이터셋의 정렬이 필요할 때, Multi-AAZ기능이 필요할 때 사용한다.
