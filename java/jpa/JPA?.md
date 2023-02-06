## JPA?
- Java Persistence API
- 자바 진영의 ORM 기술 표준

### ORM?
- Objeect-relational mapping(객체 관계 매핑)
- 객체는 객체대로 설계
- 관계형 데이터베이스는 관계형 데이터베이스대로 설계
- ORM 프레임워크가 중간에서 매핑
- 대중적인 언어들은 대부분 ORM 기술이 존재

#### JPA는 애플리케이션과 JDBC사이에서 동작

### JPA 역사
EJB - 엔티티 빈 (자바표준) -> 불편함 -> 개빈 킹이라는 개발자가 하이버네이트를 만듬 -> 자바 진영에서 개빈 킹을 데려와 ORM 표준인 JPA를 만듬

### JPA를 사용해야하는 이유
- SQL 중심적인 개발에서 객체 중심으로 개발
- 생산성
- 유지보수
- 패러다임의 불일치 해결
- 성능 최적화

#### sql에 의해 객체 탐색 범위가 결정되지 않는다. 자유롭게 객체 그래프를 탐색할 수 있다.

#### JPA 비교: 자바 컬렉션처럼 같은 값으로 객체를 조회할 경우 동일성이 보장된다.

### 성능 최적화
1. 1차 캐시와 동일성 보장
- 같은 트랜잭션 내에서는 같은 엔티티를 반환 -> 약간의 조회 성능 향상
- DB 격리 수준이 Read Commit이어도 애플리케이션에서 Repeatable Read 보장

2. 트랜잭션을 지원하는 쓰기 지연
- 트랜잭션을 커밋할 때까지 insert sql을 모은다.
- JDBC BATCH SQL 기능을 사용해서 한번에 SQL 전송
- update, delete로 인한 로우(ROW)락 시간 최소화
- 트랜잭션 커밋 시 update, delete sql 실행하고, 바로 커밋
```
 transaction.begin();
    
 changeMember(memberA);
 deleteMember(memberB);
 비즈니스_로직_수행(); // 비즈니스 로직 수행 동안 DB 로우 락이 걸리지 않는다.
    
 //커밋하는 순간 데이터베이스에 update, delete sql을 보낸다.
 transaction.commit();
```
3. 지연 로딩, 즉시 로딩
- 지연로딩: 객체가 실제 사용될 때 로딩
```
지연 로딩
Member member = jpa.find(memberId); -> select * from member
Team team = member.getTeam();
String teamName = team.getName(); -> select * from Team
```
- 즉시로딩: join sql로 한번에 연관된 객체까지 미리 조회
```
즉시 로딩
Member member = jpa.find(memberId); -> select m.*, t.* from member join team.....
Team team = member.getTeam();
String teamName = team.getName();
```