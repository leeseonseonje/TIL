## Optional
- Null을 리턴하는 것 자체가 문제

- 리턴타입으로만 사용(권장사항)
  (메소드 매개변수 타입, 맵의 키 타입, 인스턴스 필드 타입으로 쓰지 말자.)
```
(좋은 예, 리턴 타입으로 사용)
public Optional<Member> getMember() {
	return Optional.ofNullable(member);
}

(나쁜 예, 메소드 매개변수 타입)
public void setMember(Optional<Member> member) {
	// Optional의 참조 자체가 null일 수 있다. ex) setMember(null)
    // Optional자체의 널 체크를 따로 해줘야하기 때문에 Optional객체를 쓰는 의미가 없어진다.
	if (member != null) {
		member.ifPresent(m -> this.member = m); 
    }
}

(나쁜 예, 맵의 키 타입)
//맵의 키는 절대 null일 수 없다. 따라서 Optional을 쓸 필요가 없다. 쓰면 안된다.
Map<Optional<String>, Member> map = new HashMap<>();

(나쁜 예, 인스턴스 필드 타입)
public class Member {
	// 필드 타입을 optional로 사용하지 말고 getter의 리턴 타입으로 사용한다.
	private Optional<Address> address; 
}
```

- 반환값이 Optional인 메소드에서 null을 리턴하지 말자
```
public Optional<Member> getMember() {
	return null;
}

//반환할 값이 없다면 Optional.empty()를 사용한다.
//Optional.empty(): 빈 Optioanl객체 반환
public Optional<Member> getMember() {
	return Optional.empty();
}
```

- 프리미티브 타입용 Optional도 있다. (OptionalInt, OptionalLong 등등)

- Collection, Map, Stream Array, Optional은 Optional로 감싸지 않는다.
  (empty(빈 객체)를 지원하기 때문에 Optional로 감싸게되면 두번 감싸는 꼴이 된다.)