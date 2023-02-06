### 긴급 요구사항
- 검색 조건 추가
- 나이
- 이름

```
String sql = "select * from member" +
				"where name like ?" +
				"and age between ? and ?"
```

!!! 버그 있음

```
위 쿼리 문자를 합치면
"select * from memberwhere name like ?and age between ? and ?"
```

### Query의 문제점
- Query는 문자, Type-check 불가능
- 실행하기 전까지 작동여부 확인 불가

에러는 크게 2가지
- 컴파일 에러 (좋은 에러)
- 런타임 에러 (나쁜 에러)

### IF
- 만약 SQL이 클래스처럼 타입이 있고 자바 코드로 작성 할 수 있다면?
- type-safe

#### Type-safe
- 컴파일시 에러 체크 가능
- Code-assistant

### QueryDSL
- 쿼리를 Java로 type-safe하게 개발할 수 있게 지원하는 프레임워크
- 주로 JPA 쿼리(JPQL)에 사용

### QueryDSL 분석
- Domain(도메인)
- Specific(특화)
- Language(언어)

#### DSL
- 도메인 + 특화 + 언어
- 특정한 도메인에 초점을 맞춘 제한적인 표현력을 가진 컴퓨터 프로그래밍 언어
- 특징: 단수, 간결, 유창