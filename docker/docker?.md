## Docker?
- 도커는 컨테이너 기술이다. 컨테이너를 생성하고 관리하기 위한 도구다.

### Container?
- 소프트웨어 개발에서 컨테이너는 표준화된 소프트웨어 유닛이다.

- 해당 코드를 실행하는데 필요한 의존성과 도구가 포함되어 있다.

- 동일한 코드, 동일한 도구, 동일한 버전을 사용하는 컨테이너는 항상 동일한 동작과 결과를 제공한다.

- 컨테이너은 독립적이다. 다른 컨테이너와 섞이지 않는다.

- 도구가 실행되는 모든곳에서 동일한 환경에서 동일한 애플리케이션을 실행할 수 있다.

## Docker를 사용하는 이유
-  독립적인 컨테이너 안에 개발 환경을 구성하여 어느 서버에서나 동일한 동작을 보여줄 수 있다.

## vm과 container
- vm, container둘다 독립적인 환경을 구성하여 애플리케이션을 실행할 수 있다.

- vm은 많은 자원을 필요로 한다.

- 컨테이너는 작은(가벼운) 운영체제가 내제되어 있다.

- 도커 엔진을 기반으로 컨테이너를 기동할 수 있다.

- 여러개의 컨테이너로 분리할 수 있다.

- 구성 파일을 사용하여 컨테이너를 구성할 수 있다.

- 구성 파일을 다른 사람들과 공유하여 다른 사람들이 컨테이너를 다시 만들 수 있도록 하거나 이미지라 불리우는 것에 빌드할 수도 있다.

- 이미지를 다른 사람과 공유하여 모든 사람이 자신의 시스템에서 동일한 컨테이너를 시작할 수 있도록 할 수 있다.

### 컨테이너 장점
- 운영체제와 시스템에 미치는 영향이 적고, 빠르다.

- 최소한의 디스크 공간을 사용한다.

- 이미지, 구성 파일이 있기 때문에 공유, 재구축 및 배포하는 것이 매우 쉽다.

- 쓸데없는 도구 없이 애플리케이션을 실행하는데 필요한 것만 있다.

### Docker Hub
- 클라우드, 웹에서 이미지를 호스팅하여 다른 시스템과 사람들에게 쉽게 공유할 수 있게 해주는 서비스다.


## docker build
- Dockerfile을 기반으로 이미지를 빌드한다.
```
*Dockerfile*

FROM node:16 // 컨테이너에 설치할 node 버전

WORKDIR /app // 컨테이너의 해당 경로를 프로젝트 경로로 지정

COPY package.json . // 현재 경로의 package.json 복사

RUN npm install // npm install 명령어로 컨테이너에서 해당 애플리케이션에 필요한 의존성 설치

COPY . . // 소스파일 복사

EXPOSE 3000 // 포트 설정

CMD ["node", "app.mjs"] // 실행 명령여 (node app.mjs)

```

- docker build명령어를 실행한 경로에서 Dockerfile을 찾는다.

- image ID: 이미지를 빌드하면 imageID를 부여한다.


## docker run
- 빌드된 이미지로 컨테이너를 실행한다.

- -p 포트를 지정한다.
```
docker run -p 3000:3000 imageID
```