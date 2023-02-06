## Image?
- 실제로 코드와 코드를 실행하는데 필요한 도구를 포함한다.

- 이미지에는 코드, 설정 등 여러가지가 포함된다.

- 이미지를 기반으로 여러 컨테이너를 만들 수 있다.

## Container?

- 컨테이너는 이미지의 구체적인 인스턴스

## 이미지 생성하고 가져오기
- 두가지 방법이 존재한다.

- 첫 번째는 이미 존재하는 이미지를 가져오는 방법이다. (DockerHub)

- 두 번째는 자신이 이미지를 구축하는 것이다.

## Dockerfile
- 자체 이미지를 빌드할때 실행하려는 도커에 대한 설정 명령이 포함된다.

- FROM (이미지 이름): 다른 베이스 이미지(이미지 이름)에 자체 이미지를 구축할 수 있다.

- COPY (경로): 로컬에 어떤 파일이 이미지에 들어가는지 설정한다.
```
COPY는 기본적으로 두 개의 경로를 설정한다.

첫번째는 컨테이너의 외부, 이미지의 외부 경로로, 이미지로 복사되어야 할 파일들이 있는 경로를 설정한다.
- '.'을 입력할 경우 Dockerfile이 있는 경로에서 Dockerfile을 제외한 파일들을 이미지로 복사한다.

두번째는 파일을 저장할 이미지의 내부경로다.
- 모든 이미지와 컨테이너에는 완전히 독립된 자체 내부 파일 시스템이 존재한다.
- 여기에서는 도커 컨테이너의 루트 엔트리를 사용하지 않고 사용자가 선택한 서브 폴더를 사용하는 - 것이 좋다.
- 원하는 대로 이름을 지정할 수 있다.
- 도커 컨테이너 내부에 해당 경로가 존재하지 않을 경우 이미지와 컨테이너에 생성된다.
- '/app' 이라고 설정할 경우 도커 컨테이너 내부의 /app경로에 파일이 복사된다.
- COPY 설정 전에 WORKDIR 설정을 해줬다면 WORKDIR설정에 있는 경로가 기본(루트) 경로가 된다.
```

___ex) COPY . /app => Dockerfile이 있는 경로의 모든 파일이 도커 컨테이너 내부의 /app 아래에 복사된다.___

- RUN (command): 로컬 파일 복사 후 이미지에서 해당 명령을 실행한다.
```
- RUN으로 실행하는 모든 명령은 도커 컨테이너의 루트 폴더에서 실행된다.
- 따라서 COPY에서 경로를 루트 경로가 아닌 경로로 지정해줬다면, 해당 설정에서도 경로를 지정해줘야 한다.
- 해당 경로를 지정하기 위해서 모든 파일을 복사하기 전에 (COPY 설정 전에) 'WORKDIR 경로'로 경로를 설정 한다.
```

- CMD (command): 이미지를 기반으로 컨테이너가 시작될 때 실행되는 명령어를 설정한다.

#### RUN과 CMD 차이?
- RUN은 이미지를 '빌드' 할때마다 실행되는 명령어

- CMD는 빌드된 이미지를 기반으로 '컨테이너'를 띄울때 실행되는 명령어이다.

- ex) npm install같은 경우 이미지가 빌드될 때 모든 nodeJS 종속성이 설치되어야 하므로 RUN npm install을 사용해야 한다.

- node main.js같은 경우 node 서버를 실행하는 명령어이기 때문에 이미지가 빌드할때 실행할 필요가 없다. 하지만 컨테이너가 시작될 때 실행 되어야 한다. 따라서 CMD ["node", " main.js"]를 사용해야 한다.

- EXPOSE (Port): 마지막 명령전에 입력한다. 로컬 시스템에 특정 포트를 노출하고 싶다는 것을 도커에 알리는 설정이다. (별다른 효과가 있는게 아니고 단순히 알리는 것이다. 주석 같은 것)

### Dockerfile 예시
```
FROM node // 'node'라는 베이스 이미지 위에 자체 이미지를 빌드

WORKDIR /app // 기본 작업 디렉토리를 /app로 설정

COPY . /app // 첫번째 경로에 있는 로컬 파일들을 두번째 경로에 있는 도커 이미지 경로에 복사한다.

RUN npm install // 이미지가 빌드될때 해당 명령어를 실행한다.

EXPOSE 80 // 외부로 공개할 포트

CMD ["node", "server.js"] // 이미지를 기반으로 컨테이너가 실행될 때 실행하는 명령어
```
- 'docker build /Dockerfile경로' 명령어로 이미지 빌드


## Image는 읽기 전용

## Image Layer

- 도커는 이미지를 빌드할때마다 모든 명령 결과를 캐시하고 이미지를 다시 빌드할때 캐시에 결과가 있으면 캐시된 결과를 사용한다. 이것을 레이어 기반 아키텍처라고 한다.

- Dockfile의 명령어들은 모두 별도의 레이어다.

- 아래 Dokerfile을 예시로 들어보겠다.

```
FROM node

WORKDIR /app

COPY . /app

RUN npm install

CMD ["node", "server.js"]
```

- 위 Dockerfile의 명령어들을 순서대로 실행한다.

- 각 명령마다 변경사항이 없을 경우, 도커는 실행된 결과를 사용한다.

- 만약 server.js의 코드를 수정했을 경우, server.js의 파일만 변경되었기 때문에 'COPY' 명령어만 새로 수행하면 되고 나머지는 캐시된 결과를 사용하면 된다고 생각한다.

- 그런데 도커는 'RUN npm install'명령까지 새로 실행해 버린다.

- 이유는 도커는 npm install이 이전과 동일한 결과를 보여줄지 모르기 때문이다.

- 그래서 아래 처럼 Dockerfile을 바꿀 수 있다.

```
FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

CMD ["node", "server.js"]
```

- 위 Dockerfile에서는 package.json을 COPY후 npm install을 RUN 한다.

- 이렇게되면 코드가 변경 되었을때 package.json의 변화(패키지 의존성의 변화)가 없으면 npm install을 RUN하지 않고 캐시된 결과를 사용한다.

- 결과적으로 코드 변경 후 이미지를 다시 빌드하더라도 빌드 속도가 빨라지게 된다.

## run, start
- image를 컨테이너화 할 경우 -> run (attached 모드)

- container를 실행할 경우 -> start (dettached 모드)

### 대화형

- image: docker run -it

- container: docker start -a -i

## 컨테이너 파일 복사
- 컨테이너로부터 혹은 컨테이너에 파일을 복사할 수 있다.

### 컨테이너에 로컬 파일 복사

- 실행 중인 컨테이너에 docker cp [복사할 파일명] [컨테이너 이름]:[복사하려는 컨테이너 내부 경로]

    - ex) docker cp test/. container:/test
      >.은 test아래의 모든 파일이란 뜻이고, 컨테이너에 경로가 없을 경우 생성된다.

### 컨테이너에 있는 파일 로컬에 복사

- docker cp [컨테이너 이름]:[복사하려는 컨테이너 내부 경로 및 파일] [로컬에 복사할 경로]

    - ex) docker cp container:/test test

## 이미지 공유

#### Dockerfile 공유
- Dockerfile과 컨테이너에 올라갈 파일들을 공유한다.

    - Dockerfile을 가지고 이미지 빌드


- 이미지 공유
    - 빌드할 필요가 없다.

## 도커 허브
- docker push [docker hub ID/repository이름]

    - 도커 이미지의 이름이 docker hub ID/repository이름 이어야 한다.

    - ex) docker push ___seonseonje/docker-study-repository___

- 도커 허브에 push하는 방식은 이미지의 모든 파일을 push하는것이 아닌 추가 파일만 push한다.
> 예를 들어 node.js앱을 push할 경우, node.js는 이미 도커 허브에 이미지가 있기 때문에 node.js까지 push하지 않고 기존에 도커 허브에 있는 node.js이미지와 연결하여 추가된 파일(node.js 코드, 설정파일들)만 push한다.

### pull
- 도커 허브에서 이미지를 다운받을 수 있다.

- docker pull ~~
    - ex) docker pull seonseonje/docker-study-repository

- docker run을 실행할 시 로컬에 run한 이미지가 없으면 도커 허브에서 찾아서 풀링 후 실행한다.

- 만약 로컬에 이미지가 있으면 그 이미지를 바로 실행한다. (최신버전을 보장해주진 않는다)