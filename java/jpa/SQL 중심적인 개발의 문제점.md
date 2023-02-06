## SQL 중심적인 개발의 문제점
애플리케이션은 보통 객체 지향 언어를 사용

데이터베이스는 관계형 데이터베이스를 많이 사용

가장 보편적인 형태는 객체 지향 언어 + RDB (객체를 관계형 DB에 관리)

하지만 DB는 SQL만 알아들을 수 있음 이로 인해 SQL 중심적인 개발이 발생하게 된다.

무한반복 CRUD + 자바 객체를 SQL로, SQL을 자바 객체로 (지루한 코드)

객체를 CRUD할 경우에 CRUD 쿼리를 작성한다. 이 후 새로운 필드, 컬럼이 추가되면, 작성한 모든 쿼리에 추가된 필드, 컬럼을 추가해야한다.

결국 애플리케이션은 SQL에 의존적인 개발을 하게 된다.

## 패러다임의 불일치

객체 지향 프로그래밍은 추상화, 캡슐화, 정보은닉, 상속, 다양성 등 시스템의 복잡성을 제어할 수 있는 다양한 장치들을 제공한다.

객체 -> SQL 변환 -> SQL -> RDB

개발자 = SQL 매퍼가 되어버린다.

### 객체와 관계형 데이터베이스의 차이
1. 상속
2. 연관관계
3. 데이터 타입
4. 데이터 식별 방법

객체: 상속 관계
RDB: 테이블 슈퍼타입 서브타입 관계(실제 상속관게와는 다르다.)

상속구조인 객체를 DB에 저장할 경우 데이터를 분해해서 자식클래스의 데이터는 서브타입 테이블에 insert, 부모 클래스의 데이터는 슈퍼타입 테이블에 insert를, 두번으로 쪼개서 insert를 해야한다.

데이터를 조회할 경우에 join을 해야한다.

복잡하다.

### 자바 컬렉션에 조회하면?
```
저장: list.add(child);

조회: Child child = list.get(childId);
	 Parent parent = list.get(childId); (다형성 활용)
```

### 연관관계
- 객체는 참초를 사용: member.getTeam()

- 테이블은 외래 키를 사용: join on m.team_id = t.team_id

#### 객체를 테이블에 맞추어 모델링
```
class Member {
	String id;
    Long teamId;
    String username; 
}

class Team {
	Long id;
    String name;
}

SQL: insert into member(member_id, team_id, username) values..... 
```
#### 객체다운 모델링
```
class Member {
	String id;
    Team team;
    String username;
    
    Team getTeam() {
    	return team;
    }
}

class Team {
	Long id;
    String name;
}

SQL: member.getTeam().getId{();
	insert into member(member_id, team_id, username) values.....
```

#### 객체 모델링 조회
```
select m.*, t.* from member m join team t on m.team_id = t.team_id

public Member find(String memberId) {
	//SQL 실행
	Member member = new Member();
    //DB에서 조회한 회원 관련 정보를 모두 입력
    
    Team team = new Team();
    //DB에서 조회한 팀 관련 정보를 모두 입력
    
    //회원과 팀 관계 설정
    member.setTeam(team);
    return member;
}
```

#### 객체 모델링, 자바 컬렉션에서 관리를 한다면?

```
list.add(member);

Member member = list.get(memberId);
Team team = member.getTeam();
```

#### 객체는 자유롭게 객체 그래프를 탐색할 수 있어야 한다.

SQL을 사용하는 순간 처음 실행하는 SQL에 따라 탐색 범위가 결정된다.

ex)
```
첫 SQL
select m.*, t.* from member m join team t on m.team_id = t.team_id

member.getTeam(); // OK

member.getOrder(); // null

??: select로 team만 조회해서 member객체에 저장, order는 당연히 null (객체 그래프 자유롭게 탐색 불가능)

객체 그래프 탐색이 SQL에 영향을 받게 된다.
```

#### 모든 객체를 미리 로딩할 수는 없다
상황에 따라 동일한 회원 조회 메서드를 여러벌 생성
```
1. memberDAO.getMember(); // Member

2. memberDAO.getMemberWithTeam(); // Member, Team

3. memberDAO.getMemberWithOrderWithDelivery(); // Member, Order, Delivery
```

*결론: 실행된 쿼리에 따라 객체 그래프 탐색의 범위가 정해진다.*

#### 비교

쿼리로 조회한 member 2개
```
member1 == member2 // 다르다
```

컬렉션에서 조회
```
Member member1 = list.get(memberId);
Member member2 = list.get(memberId);
member1 == member2 // 같다
```

*객체답게 모델링 할수록 매핑 작업만 늘어난다.*

객체를 자바 컬렉션에 저장 하듯이 DB에 저장할 수는 없을까?? -> JPA