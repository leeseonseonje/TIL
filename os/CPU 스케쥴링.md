### CPU Scheduling
- 멀티 프로그래밍에선 필수

- CPU의 이용성(컨텍스트 스위치, 타임 쉐어링)등을 위해선 CPU 스케쥴링이 필수다.

### 프로세스 상태
- CPU burst: running 상태

- I/O burst: waiting, ready 상태

CPU bound: cpu burst가 많은 경우

I/O bound: i/o burst가 많은 경우

#### I/O bound가 CPU bound보다 빈도가 많은 경우 CPU의 스케쥴링이 제대로 동작하여 CPU의 효율이 높아진다.

### CPU 스케쥴링을 만들 때
- ready상태에 있는 프로세스들 중에서 CPU를 할당해줄 수 있는 프로세스를 선택 해야한다.

### next Process?
우선순위 큐

### Preemptive(선점형) vs Non-Preemptive(비선점형)
- 선점형: 쫓아낼 수 있다.

- 비선점형: 못 쫓아 낸다. (자발적으로 나온다)

- 비선점형 스케쥴링: 어떤 프로세스가 CPU를 선점하고 나면 그 프로세스가 릴리즈 할 때 까지 계속 CPU를 사용한다.

- 선점형 스케줄링: 스케쥴러가 어떤 이유에 의해 CPU를 선점하고 있는 프로세스를 쫓아낼 수 있다.

### CPU 스케쥴링 의사결정
4가지 경우가 있다.

1. running 상태에서 waiting 상태로 가는 경우
2. running 상태에서 ready 상태로 가는 경우
3. waiting 상태에서 ready 상태로 가는 경우
4. terminates

1번, 4번 경우는 비선점형
2번, 3번 경우는 선점형

### Dispatcher
- CPU 코어의 제어를 넘겨 주는 것

- 컨텍스트 스위치를 해주는 모듈

디스패처가 하는 일은 컨텍스트를 하나의 프로세스에서 다른 프로세스로 넘겨 주고, 사용자 모드 바꿔준다.

#### 스케쥴러는 어떤 프로세스를 변경할지 선택하고, 실제로 스위칭을 해주는 것은 디스패처다.

### 스케쥴링 목표

- CPU가 놀지 않고 열심히 일하게 하도록 한다.

- Throughput을 목표로 한다.
    - Throughput? 완료되는 프로세스의 수

- Turnaround Time
    - 어떤 프로세스의 실행에서 종료까지의 시간

- Waiting Time
    - 프로세스가 레디큐에서 대기하고 있는 시간을 최소화

- Response Time
    - 응답 시간 최소화

### 스케쥴링 알고리즘

- FCFS: First-Come, First-Served (문제가 많다 초창기시절 알고리즘)
    - 먼저 온거 부터 처리


- SJF: Shortest Job First
    - 작업시간이 짧은거 부터 처리


- RR: Round Robin
    - Time Sharing을 해서 정해진 시간 만큼만 수행하는 방식 (가장 현대적)


- Priority-based
    - Round Robin을 사용, 다음 프로세스의 대상을 우선순위를 부여해 선택

- MLQ
    - 동적으로 적용

- MLFQ
    - 동적으로 적용, 피드백 기능, 하다 안되면 방식 변경