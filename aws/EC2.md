<!-- @format -->

## EC2

-   Elastic Compute Cloud (EC2)

-   클라우드 환경에서 크기가 유연하게 변경되는 기능을 제공

### 지불 방법

1. On-demand: 시간 단위로 가격이 고정되어 있다. (개발, 테스트시 사용)

    - 개발 기간이 정해져 있지 않을 경우 유용

2. Reserved: 일정량을 대여해서 사용

    - 개발 기간이 정해져 있을 경우 유용

3. Spot: 사용자가 제시한 가격보다 인스턴스 시장 가격이 높아지게 되면 인스턴스가 종료되고, 낮아질 때 이용할 수 있다.

## EBS

-   Elastic Bolck Storage

-   저장 공간이 생성되어지며 EC2 인스턴스에 있다.

-   디스크 볼륨 위에 File System이 생성된다.

### EBS 볼륨 타입

-   SSD 군과 HDD 군이 있다.

### SSD 군

-   General Purpose SSD (GP2): 최대 10K IOPS 지원, 1GB당 3IOPS속도

    -   가장 보편적인 SSD 볼륨 타입

-   Provisioned IOPS SSD (IO1): 극도의 I/O률을 요구하는(대용량 데이터베이스) 환경에서 주로 사용된다. 10K 이상의 IOPS를 지원한다.

### Magnetic/HDD 군

-   Throughput Optimized HDD (ST1): 빅데이터 보관, 컴퓨터 로그 파일 보관 등에 사용 된다. (Boot volume으로 사용 불가)

-   CDD HDD(SC1): 파일 서버와 같이 드문 volume 접근 시 주로 사용된다. 가격이 저렴하다. (Boot volume으로 사용 불가)

-   Magnetic(Standard): 가격이 가장 저렴하다. Boot volumed으로 사용 가능하다.

## ELB

-   Elastic Load Balancers

-   서버의 흐름을 균형있게 흘려보내는데 중추적인 역할을 한다.

-   하나의 서버로 traffic이 몰리는 병목현상 방지

### ALB

-   Application Load Balancers

-   OSI Layer7에서 작동된다.

-   http, https와 같은 traffic의 load balancing에 가장 적합하다.

-   request 라우팅 설정을 통하여 특성 서버에 request를 보낼 수 있다. (루트 변경)

### NLB

-   Network Load Balancers

-   OIS Layer4에서 작동된다.

-   TCP traffic에서 적합하다.

-   초당 수백만개의 request를 빠르게 처리할 수 있다.

### CLB

-   Classic Load Balancers

-   Legacy ELB

-   거의 쓰이지 않는다.

### 504 Error

-   504 Gateway Time-out

-   ELB는 에러를 발견하면 에러메세지를 제공한다. (504)

-   어플리케이션이나 서버가 응답을 받지 못하면 발생하는 에러다.

### X-Forwarded-For 헤더

-   public ip가 elb에 request, elb는 request를 private ip로 인식하게 된다. 그리고 elb는 request를 ec2로 전송하게 된다.

-   ec2는 private ip밖에 볼 수가 없다.

-   ec2에서 X-Forwarded-For 헤더를 통해 해당 request의 출처를(public ip) 확인 할 수 있다.

## Route53

-   AWS에서 제공하는 DNS 서비스

-   EC2 instance, S3 Bucket, Load Balancer 연결
