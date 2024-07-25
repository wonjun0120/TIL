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
- 호스트 볼륨 사용
    - 호스트의 디렉토리를 컨테이너의 특정 경로에 마운트