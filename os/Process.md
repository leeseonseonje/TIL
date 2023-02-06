## Process?
실행중인 프로그램
운영체제의 작업의 단위는  프로세스
하나의 프로세스가 실행되기 위해서는 여러가지 자원들이 필요하다
- CPU Time
- Memory
- files And I/O devices

컴퓨터는 CPU - Memory 구조
Memory에있는 명령들을 CPU가 하나씩 fetch하여 execute하는것이 컴퓨터의 일반적인 구조
(폰노이만 아키텍처)

프로그램들은 HDD또는 SDD같은 스토리지에 저장되어있다.
CPU는 이 스토리지에 저장되어있는 프로그램을 다이렉트로 실행할 수 없다.
프로그램(명령어들의 집합)을 메모리에 로드하여 CPU가 fetch하여 실행할 수 있다.
이러한 상태에 있는 프로그램(메모리에 로드된 프로그램)을 Process(프로세스)라고 한다.
CPU점유, 파일시스템, 입출력장치

## Memory Layout
Text Section
- 명령어들의 모음

Data Section
- 전역 변수

Heap Section
- 객체

Stack Section
- 함수 호출(함수내의 파라미터, 지역 변수 등)


### OS는 프로세스를 관리한다.

## Process State

New: 프로세스가 생성된 상태

Running: CPU를 점유하여 프로세스의 명령어가 CPU에 로드되어 실행되는 상태

Waiting: 다른 프로세스의 CPU점유를 기다리고 있는 상태

Ready: CPU점유를 할수있도록 준비가 완료된 상태

Terminated: 모든 작업이 끝나 종료된 상태

** Waiting, Ready 차이 *
- Waiting: I/O작업이 있을경우 I/O 작업이 끝날때 까지 기다리는 상태
- Ready: I/O작업이 끝나면 Waiting 상태에서 Ready상태가 되는데, Ready상태가 되면 언제든지 CPU를 점유할 수 있게 된다. 즉, Running 상태에서 Process가 실행되다 I/O 작업이 있을경우 Waiting 상태로 전환되어 I/O작업의 완료를 기다리게 된다. I/O작업이 끝나게 되면 다시 CPU를 점유 하여 Process를 실행(Running 상태)해야 하므로 CPU를 점유 할 수 있는 상태인 Ready상태로 전환 된다. 이 후 CPU를 점유하여 Running상태가 된다.
- Flow: New -> Running -> I/O -> Waiting -> Ready -> Running -> Treminated

## PCB(Process Control Block)
## or
## TCB(Task Control Block)

PCB: 각 프로세스가 가져야할 정보를 운영체제가 PCB에 저장 후 프로세스를 핸들링

PCB의 정보
- Process State
- Program Counter
- CPU registers(IR, DR 등)
- CPU Scheduling Infomation
- Memory-Management Information
- Accounting Infomation
- I/O Status Information

## Multi Processing, Multi Tasking
Single Thread 방식은 한번에 하나의 Task밖에 수행할 수 없다.
여러개를 동시에 실행해주는것을 Multi Processing, Multi Tasking이라고 한다.
Multi Processing, Multi Tasking은 O/S의 가장 핵심적인 기능이다.

Process안에서도 Single Thread방식으로 부족할 수 있다.
하나의 프로그램 내에서도 여러 Thread가 동시에 실행될 수 있다.

그것을 Thread라고 한다. 위의 Single Thread와는 다른 의미이다.

하나의 Process내에서 Process보다 더 작은 단위로 나눈게 Thread다.

요즘 대부분 Multi Thread방식으로 프로그래밍한다.

## Multi Processing
목적: 동시에 여러개의 Process를 실행 시켜보자.
이유: CPU를 효율적으로 사용하기 위해

### Time Sharing
Process간의 스위칭을 해서 사용자 입장에서 볼때, 각 프로그램이 동시에 실행되는것 처럼 보이게 하기 위함

실제로는 동시에 실행되는것이 아니라 여러개의 Process가 스위칭을 하면서 실행되는것이다.

ex)유튜브를 보면서 게임을할때 CPU의 처리속도가 빨라 두개의 작업이 동시에 실행되는것처럼 보인다.

## CPU Scheduling
Scheduling Queue
- CPU는 하나기 때문에 대기열이 있어야한다.
- 대기열에서 대기하고 있다가 CPU를 획득하는 방식이다.

### Ready Queue, Wait Queue
여러개의 프로세스는 Queue(대기열)에 저장되어 대기한다.
대기하다 CPU를 얻게되면 그때 Process가 실행된다.
이러한 대기열을 Ready Queue라고 한다.

이 후 Running상태에서 CPU의 Time이 끝나면 Ready Queue에 다시 저장되어 대기를 하게 된다.

위 경우와 달리 Running상태에서 Ready상태가 아닌, Waiting 상태가 되는 경우도 있다.
I/O Completion을 기다리고 있는 상태이다. 이러한 상태를 저장하는 대기열이 Wait Queue다. 이렇게 I/O작업이 끝나게되면 다시 Ready Queue에 저장되고 CPU 점유를 대기하게 된다.

## Queue Diagram
- I/O Request
- Time Slice Expired
- Fork a Child
- Wait for an Interrupt
  위의 작업이 발생하면 Ready Queue에 해당 프로세스가 저장되고 CPU 점유를 대기하는 상태가 된다.

## Context Switch (문맥 교환)
Context란 Process가 사용되고 있는 상태를 Context라고 한다.
이러한 Process의 상태는 PCB에 저장되어 있다.

Context Switch란 어떠한 Task가 CPU를 다른 Process한테 넘겨주는 행위다.
- 현재 Process의 상태(PCB)를 저장하고, 새로운 Process의 상태(PCB)를 보관한다.

### ex) P0와 P1의 Context Switch
P0가 실행되는 중 인터럽트가 발생할 경우 P0의 PCB정보가 저장된다.
그리고 P1의 PCB를 reload하게되며 P1이 실행되게 된다.
P1이 실행되는 중 인터럽트가 발생할 경우 P1의 PCB정보가 저장되고, 저장 해두었던 P0의 PCB reload하여 P0를 실행하게 된다.

Time Sharing, Multi Processing은 결국 OS Scheduling에 의해서 Context Switch로 이루어 지게되는 것이다.

## fork()
OS의 System Call 자식 Process를 생성해주는 함수다.