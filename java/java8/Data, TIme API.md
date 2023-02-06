## 자바8 이전의 Date
- 자바8 이전까지 사용하던 java.util.date 클래스는 mutable하기 때문에 thread safe하지 않다. (Setter)

```
Date date = new Date();

Thread.sleep(5000);

Date date2 = new Date();
System.out.println(date2); // date의 날짜보다 5초 후의 날짜를 출력

date2.setTime(date.getTime());
System.out.println(date2); // date와 동일한 날짜 출력 mutable하다.
```

- 클래스 이름이 명확하지 않다. Date인데 Time까지 다룬다.

- 월이 0부터 시작한다. (0이 1월이다.)

- type safe하지 않다. (매개변수로 받는 타입이 int형이다. 아무 정수나 들어올 수 있다.)

## 기계용1 시간, 인류용 시간
- 기계용 시간은 EPOCK (1970년 1월 1일 0시 0분 0초)부터 현재까지의 타임스탬프를
  표현한다.

- 인류용 시간은 우리가 흔히 사용하는 연,월,일,시,분,초 등을 표현한다.

- 타임스탬프는 Instant를 사용한다.

- 특정 날짜(LocalDate), 시간(LocalTime), 일시(LocalDateTime)를 사용할 수 있다.

- 기간을 표현할 때는 Duration(시간 기반)과 Period(날짜 기반)를 사용할 수 있다.
  _ ex) 30초 마다: Duration, 하루 마다:Period
- DateTimeFormatter를 사용해서 일시를 특정한 문자열로 포매팅할 수 있다.