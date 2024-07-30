# Docker 2

## 도커 컨테이너 다루기
```shell
docker exec [container] [command]
docker exec -i -t my-nginx bash     # bash shell 접속
docker exec my-nginx env            # 컨테이너 환경변수 확인
```
- exec : 실행중인 컨테이너에 명령어 실행

## 네트워크
- docker0 : 도커 엔진에 의해 기본 생성되는 브릿지 네트워크
    - veth와 eth간 다리역할
- eth0 : 호스트에서 사용하는 기본 네트워크
- veth : virtual eth, 컨테이너 내부 eth

### 컨테이너 포트 노출
```shell
docker run -p [Host_IP_Port]:[Container_Port] [container]
```

### expose vs publish
```shell
docker run -d --expose 80 nginx # 문서화용도
docker run -d -p 80 nginx       # publish 옵션은 실제 바인딩
```

### 도커 네트워크 드라이버
- Native Drivers
    - Single Host Networking
        - Bridge
            - docker0 : 기본 네트워크
            - user defined : 사용자 정의
        - Host
            - 포트바인딩 사용하지 않아도 접속 가능
        - None
            - 컨테이너에서 네트워크 기능이 필요없거나, 커스텀시 사용
    - Multi Host Networking
        - Overlay (docker swarm 사용시)
- Remote Drivers
    - 3rd Party Plugins
```shell
docker network ls
```

## 도커 컨테이너 볼륨
### 도커 레이어 아키텍처
- container layer
    - Read Write 권한
    - container 종료시 함께 삭제, 임시 저장소
- image layer
    - `docker build -t app .` 실행시 Dockerfile기반으로 이미지 빌드
    - Read only
    - 여러 레이어로 구성, 변경이 있는 경우 해당 레이어만 수정하면 됨, 저장공간 효율

### container layer가 임시 저장공간 -> 컨테이너의 영구 볼륨
- 볼륨 사용안하는 경우 데이터 영구 저장 불가
- 컨테이너 종료 후 실행하면 데이터 삭제됨 -> 해결을 위해 볼륨 사용
- 호스트 볼륨 사용
    - 호스트의 디렉토리를 컨테이너의 특정 경로에 마운트
```shell
docker run -d --name nginx \
-v /opt/html:/user/share/nginx/html \   # 호스트의 /opt/html디렉토리를 Nginx의 웹 루트 디렉토리로 마운트, 호스트:컨테이너
nginx
```
- 볼륨 컨테이너
    - 특정 컨테이너의 볼륨 마운트를 공유
    - Container의 data -> Data-only Container(볼륨 컨테이너)의 data(마운트)
    - 컨테이너 실행시 볼륨 컨테이너 지정하여 실행

```shell
# 볼륨 컨테이너, 볼륨 마운트
docker run -d --name my-volume \
-it\
-v /opt/html:/usr/share/nginx/html \
ubuntu:focal
# 볼륨 컨테이너의 볼륨 마운트 사용
docker run -d --name nginx \ 
--volumes-from my-volume \ 
nginx
```

- 도커 볼륨
    - 도커가 제공하는 볼륨 관리 기능 활용, 데이터 보존
    - `/var/lib/docker/volums/${volume-name}/_data`에 저장
```shell
# web-volume 도커 볼륨 생성
docker volume create --name db
# 도커의 web-volume 볼륨을 Mysql 웹 루트 디렉토리에 마운트
docker run -d --name app-mysql \
-v db:/var/lib/mysql \
-p 3306:3306 \
mysql
```