## Stream

- 가지고 있는 연속된 데이터를 처리하는 오퍼레이션

- 컨베이어 벨트

- 데이터를 담는 저장소(컬렉션)가 아니다.

- Funtional in nature, 스트림이 처리하는 데이터 소스를 변경하지 않는다.
    - 스트림을 사용한다고 해서 기존의 데이터를 변경하지 않는다.

    ```
    List<String> numbers = List.of("one", "two", "three", "four");
    
    stram<String> numberStream = numbers.stream().map(String::toUpperCase); // 새로운 스트림 인스턴스 생성
    
    numbers.forEach(System.out::println); // 기존의 numbers가 대문자로 바뀌지 않는다.
    ```

- 스트림으로 처리하는 데이터는 오직 한번만 처리한다.

- 중개 오퍼레이션은 근본적으로 lazy 하다.
  중개 오퍼레이션: 계속해서 스트림 연산을 할 수 있는 오퍼레이션 (Stream을 리턴한다)
  종료 오퍼레이션: 최종 연산에 사용되는 오퍼레이션 (Stream을 리턴하지 않는다.)

 ```
numbers.stream().map(s -> {
 	System.out.println(s);
  	return s.toUpperCase();
  }); //  
 ```

- 스프림 파이프라인: 0 또는 다수의 중개 오퍼레이션과 한개의 종료 오퍼레이션으로 구성된다.

- 스트림의 데이터 소스는 오직 터미널 오퍼네이션을 실행할 때에만 처리한다.

## 병렬 처리 단점
- 병렬 처리가 무조건 좋은것이 아니다.

- 쓰레드를 만드는 비용

- 쓰레드 간의 컨텍스트 스위칭 비용

- 위와 같은 이유들 때문에 병렬처리가 오히려 더 느릴수도 있다.

- 데이터가 굉장히 큰 경우 병렬처리의 의미가 있다.