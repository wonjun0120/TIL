# Docker

## 구성요소
- client
    - docker 명령어가 클라이언트 역할
- docker host
    - docker daemon = docker engin
        - 도커 엔진이 띄워진 서버 = 도커 호스트  
    - containers
        - 이미지 실행 -> 컨테이너
        - 호스트와 다른 컨테이너로부터 격리된 시스템 자원과 네트워크를 사용하는 프로세스
        - 이미지는 읽기 전용으로 사용, 변경사항은 컨테이너 계층에 저장
    - images
        - 이미지 가져올 때 registry사용
        - 컨테이너 생성시 필요한 요소
        - 컨테이너의 목적에 맞는 바이너리와 의존성 설치
        - 여러 개의 계층으로 된 바이너리 파일로 존재
- registry
    - 이미지 저장소
- docker file -> docker image -> docker container

## 도커 이미지 이름 구성
- 저장소 이름 | 이미지 이름 | 이미지 태그
- ex) wonjun0120/nginx:1.21
- 태그 생략시 : latest, 최신버전
- 저장소 생략시 : 도커허브

## 도커 이미지 저장소
- 도커 이미지를 관리하고 공유하기 위한 서버 어플리케이션
- Public, Private 구분
- Docker hub, QUAY -> public
- docker Registry, AWS ECR -> private
    - open source docker registry 직접 띄워서 사용 가능
    - private한 도커 이미지 저장소 필요한 경우 있음

## 도커 컨테이너 라이프사이클
- Created / Running / Paused / Stopped / Deleted

### 컨테이너 시작
- 이미지가 없을 경우 자동으로 pull을 먼저 수행, 이미지 다운 받음
```shell
# 1
docker create [image]       # 컨테이너 생성
docker start [container]    # 컨테이너 시작
# 2
docker run [image]          # 컨테이너 생성 및 시작
```
- 컨테이너 시작 주요 옵션
```shell
docker run \
    -i \ # 호스트의 표준 입력을 컨테이너와 연결
    -t \ # TTY 할당, -it 로 사용, 컨테이너에서 실행되는 어플리케이션이 키보드 입력이 필요한 경우 사용 
    --rm \                                      # 컨테이너 실행 종료 후 자동 삭제
    -d \                                        # 백그라운드 모드 실행
    --name [name] \                             # 컨테이너 이름 지정
    -p [host_port]:[container_port] \           # 호스트 - 컨테이너간 포트 바인딩
    -v [volum_path] \                           # 호스트 - 컨테이너간 볼륨 바인딩
    [image] \                                   # 실행할 이미지
    [command]                                   # 컨테이너 내에서 실행할 명령어
```

- 컨테이너 상태 확인
```shell
docker ps                   # 실행중인 컨테이너 상태 확인
docker inspect [container]  # 컨테이너 상세 정보 확인
docker ps -a                # 전체 컨테이너 상태 확인

# 응용 - 모든 실행중인 컨테이너 중지
docker stop $(docker ps -a -q)
```

- 컨테이너 삭제
```shell
docker rm [continer]        # 컨테이너 삭제 (실행중인 컨테이너 불가)
docker run --rm ...         # 컨테이너 실행 종료 후 자동 삭제
docker rm -f [container]    # 컨테이너 강제 종료 후 삭제 (SIGKILL)
docker container prune      # 중지된 모든 컨테이너 삭제
```

## 엔트리포인트와 커멘드
- 엔트리포인트
    - 도커 컨테이너가 실행할 때 고정적으로 실행되는 스크립트 혹은 명령어
    - 생략 가능, 생략하는 경우 커멘드에 지정된 명령어로 수행
- 커멘드
    - 도커 컨테이너가 실행할 떄 수행할 명령어 혹은 엔트리포인트에 지정된 명령어에 대한 인자값
- \[Entrypoint\]\[Command\]

## 도커 컨테이너 환경변수
- `variable.env` 형식의 파일 생성
- `docker run --env-file`로 파일 지정 가능