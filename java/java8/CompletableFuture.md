## CompletableFuture
- 자바에서 비동기 프로그래밍을 가능케 하는 인터페이스
```
Future에서 하기 어려운 것들

- Future를 외부에서 완료 시킬 수 없다. 취소하거나, get()에 타임아웃을 설정할 수는
  있다.
  
- 블로킹 코드(get())를 사용하지 않고서는 작업이 끝났을 때 콜백을 실행할 수 없다.

- 여러 Future를 조합할 수 없다, 예) Event 정보 가져온 다음 Event에 참석하는 회원 목록
  가져오기
  
- 예외 처리용 API를 제공하지 않는다.
```

- implements Future

- implements CompletionStage

- future.join(): 예외 발생 시 언체크드 익셉션

- future.get(): 예외 발생 시  체크드 익셉션

### 비동기로 작업 실행하기
- 리턴값이 없는 경우: runAsync()

- 리턴값이 있는 경우: supplyAsync()

- 원하는 Executor(쓰레드풀)를 사용해서 실행할 수도 있다. (기본은ForkJoinPool.commonPool())

### 콜백 실행하기
- thenApply(Function)

- thenAccept(Consumer)

- thenRun(Runnable)

- 콜백 자체를 또 다른 쓰레드에서 실행할 수 있다.

### 쓰레드를 생성하지 않고 CompletableFuture를 실행할 수 있는 이유?

#### ForkJoinPool
- Java7 부터 도입 되었다.

- Executor를 구현한 구현체 중 하나다.

- Task의 크기에 따라 분할(Fork)하고, 분할된 Task가 처리되면 그것을 합쳐(Join) 리턴해준다.

### 조합하기
- thenCompose(): 두 작업이 서로 이어서 실행하도록 조합

- thenCombine(): 두 작업을 독립적으로 실행하고 둘 다 종료 했을 때 콜백 실행

- allOf(): 여러 작업을 모두 실행하고 모든 작업 결과에 콜백 실행

- anyOf(): 여러 작업 중에 가장 빨리 끝난 하나의 결과에 콜백 실행 