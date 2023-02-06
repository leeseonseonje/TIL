## Concurrent 소프트웨어
- 동시에 여러 작업을 할 수 있는 소프트웨어

- 자바에서는 멀티프로세싱(ProcessBuilder), 멀티쓰레드를 지원한다.

- 자바 멀티쓰레드 프로그래밍 ___(Thread / Runnable)___

- 쓰레드 순서는 보장되지 않는다.

## Executor
- 고수준 Concurrency 프로그래밍
```
- 쓰레드를 만들고 관리하는 작업을 애플리케이션에서 분리

- 그런 기능을 Executors에게 위임
```

- Executor가 하는 일
```
- 쓰레드 만들기: 애플리케이션이 사용할 쓰레드 풀을 만들어 관리한다.

- 쓰레드 관리: 쓰레드 생명 주기를 관리한다.

- 작업 처리 및 실행: 쓰레드로 실행할 작업을 제공할 수 있는 API를 제공한다.
```

- 쓰레드 풀을 생성한다.

- ExecutorService에는 BolckingQueue라는게 존재한다.
```
BolckingQueue?

- 쓰레드풀에 있는 쓰레드의 갯수보다 작업량이 많을 경우, Queue에서 쓰레드를 대기한다.

- 예를 들어, 쓰레드 풀에 쓰레드가 2개밖에 없는데 작업량이 10개인 경우, 쓰레드가 2개의 작업을 맡아서 처리하게 되고
나머지 8개의 작업은 Queue에 대기한다. 처음 맡은 2개의 작업이 끝나면 Queue에 대기하고 있던 작업들을 꺼내 작업을
시작한다.
```

- ScheduledExecutorService: 시간 단위로 쓰레드를 실행할 수 있다.
```
ScheduledExecutorService executorService=Executors.newSingleThreadScheduledExecutor();
executorService.scheduleAtFixedRate(
		() -> System.out.println("scheduled: " + Thread.currentThread().getName(),
        1, // 1초 후
        3, // 3초 마다 실행
        TimeUnit.SECONDS // 시간 단위
	);
}
```

## Callable Future
### Callable
- Runnable과 유사하지만 작업의 결과를 받을 수 있다.

### Future
- 비동기적인 작업의 현재 상태를 조회하거나 결과를 가져올 수 있다.

-  future.get(): callable에서 return한 값을 꺼낸다.

- isDone: 작업이 끝났는지 여부
```
- true: 작업이 끝남

- false: 작업이 끝나지 않음
```

- cancel: 작업 취소 (true: 현재 진행중인 작업을 인터럽트 하고 종료, false: 현재 진행중인 작업을 기다렸다 종료)

```
- true: 현재 진행중인 작업을 인터럽트 하고 종료

- false: 현재 진행 중인 작업을 기다렸다 종료

get()을 할 수 없다, isDone은 무조건 true다.

### done이 true인건 값을 가져갈 수 있다라는 뜻이 아닌, 단순히 작업을 종료했다는 뜻이다.
```

- invokeAll: 모든 쓰레드의 작업들이 모두 끝날때까지 기다린다.
```
        ExecutorService executorService = Executors.newSingleThreadExecutor();

        Callable<String> hello = () -> {
            Thread.sleep(2000L);
            return "hello";
        };

        Callable<String> java = () -> {
            Thread.sleep(3000L);
            return "java";
        };

        Callable<String> seon = () -> {
            Thread.sleep(1000L);
            return "seon";
        };

        List<Future<String>> futures = executorService.invokeAll(
        List.of(hello, java, seon)
        );
        for (Future<String> future : futures) {
            System.out.println(future.get());
        }
//3개의 callable이 모두 끝나야 blocking이 풀린다.
//3개의 callable이 return하는 값이 한꺼번에 출력된다.
```

- invokeAny: 모든 callable을 기다리지 않고 가장 먼저 끝난 작업의 값만 반환받는다.