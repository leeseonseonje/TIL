프로세스들의 동시성이 보장되게 실행되기 위해선 각각의 프로세스가 독립적으로 실행되는 경우와, 서로 협력하면서 실행되는 경우다.

independent: 각각의 프로세스가 독립적으로 실행 (CPU 스케쥴링만 잘 되어 있으면 문제없음)
cooperating: 프로세스들이 협력 (협력하는 과정중에 문제가 발생)

따라서 cooperating 프로세스들은 IPC메커니즘이 필요하다.

IPC 두가지 모델
- Shared Memory(공유 메모리)
- Message Passing

### 생산자 - 소비자 문제
협력 프로세스들간의 가장 기본적인 문제다.
- 생산자는 정보를 생산하고, 소비자는 정보를 소비한다.
- ex) C 컴파일러 -> 어셈블러 -> 어셈블러 컴파일러 -> 기계어
- ex) 웹서버(HTML 생산)생산자, 브라우저(HTML 화면에 뿌려줌) 소비자
- ex) 유튜브 서버: 동영상 실시간 스트리밍(생산자), 스마트폰(클라이언트): 화면에 영상 표시(소비자)

공유 메모리를 사용했을때
생산자, 소비자가 동시에 실행된다.

Buffer를 사용하면된다.
생산자는 Buffer를 채우고, 소비자는 Buffer를 비운다.


### Massege Passing
Shared Memory 방식은 애플리케이션 개발자가 Shared Memory를 직접 구현해야하는 단점이 있음 이러한 단점을 보완 하기 위해 O/S가 message Passing이라는 기능 제공
System call 제공: send(), receive()

Communication Links:

협력하는 프로세스간의 커뮤니케이션
send, receive 메세지
direct, indirect
synchronous, asynchronous
automatic, explicit buffering

dircet communication: 메세지를 보내는 프로세스, 받는 프로세스를 명시적으로 선언해줘여함.

다이렉트 커뮤니케이션에서 가장 중요한것은 누구에게 보내는지, 누구에게 받는지 명시를 해줘야함
명시를 해주기 때문에 다이렉트 커뮤니케이션 링크는 자동적으로 생성된다.
이 다이렉트 커뮤니케이션 링크는 두개의 프로세스 사이의 하나의 링크만 존재할 수 있다.
send(P, message): message를 p에게 준다.
receive(Q, message): message를 q에게 받는다.

indirect communication: 두개의 프로세스사이를 이어주는 매게체가 존재한다.

인다이렉트 커뮤니케이션은 mailbox를 통해서 메세지를 전송하고 수신한다.
요즘에는 mailbox라는 용어보다 port라는 용어를 사용한다.

PORT
- 메세지를 보내는 저장소
- 메세지를 받는 저장소

send(A, message): port A에 message를 보냄
receive(A, message): port A에서 message를 가져감

두 개의 프로세스가 port를 공유할때 이 두 프로세스간의 링크가 생성된다.
이러한 특성 때문에 여러개의 프로세스가 통신할 수 있다.

OS는 port create
send, Receive message
port delete 기능 제공해줘야한다.

### blocking, non-blocking: synchronous, asynchronous

Blocking Send: message 수신자가 receive를 할 때 까지 message 전송자가 블락됨

Non-Blocking Send: message 전송자는 send만 한 후 다른 작업들을 진행할 수 있다.

Blocking Receive: 전송 받은 메세지를 다 receive할 때 까지 message 수신자는 블락됨

Non-Blocking Receive: message 수신자는 message를 수신 받으면서 다른 작업들을 계속해서 진행 할 수 있다.

synchronous: blocking 방식 동기
asynchronous: non-blocking 비동기