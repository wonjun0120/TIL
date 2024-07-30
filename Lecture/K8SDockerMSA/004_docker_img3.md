# Docker 3
## 컨테이너 Log 관리
### 표준 출력과 표준 오류
- STDOUT / STDERR
- 도커 컨테이너에서 로그를 다루기 위해서는 애플리케이션에서 로그를 표준 출력과 표준 오류로 내보내는 것을 표준으로 해야함
- 도커에서는 앱에서 내보낸 표준 출력과 오류를 `logging driver`로 처리
- 도커에서는 많은 종류의 로깅 드라이버를 제공

### 로그 확인하기
```shell
docker logs [container]             # 전체 로그 확인
docker logs --tail 10 [container]   # 마지막 10줄 로그 확인
docker logs -f [container]          # 실시간 로그 스트림 확인
docker logs -f -t [container]       # 로그마다 타임 스탬프 표시
```

### 호스트 운영체제의 로그 저장 경로
- logging driver -> json-file
```shell
cat /var/lib/docker/containers/${CONTAINER_ID}/${CONTAINER_ID}-json.log
```

### 로그 용량 제한하기
- 컨테이너 단위로 로그 용량을 제한할 수 있음
- 도커 엔진에서 기본 설정 진행 가능
```shell
docker run \
-d \
--log-driver=json-file \    # 로그 드라이버 설정
--log-opt max-size=3m \     # 한 로그 파일당 크기 3M제한
--log-opt max-file=5 \      # 최대 로그 파일 3개
nginx
```

## 도커 이미지 관리
### 도커 이미지 구조
- 도커 이미지 구조
    - 레이어 구조
- 도커 컨테이너
    - 도커 이미지는 컨테이너에 이미지 레이어에 read only로 복사, 변경 불가
    - 컨테이너 레이어는 read/writer 가능, 컨테이너 삭제시 같이 삭제됨

### Dockerfile 없이 이미지 생성
- 기존 컨테이너 기반으로 이미지 생성 가능
```shell
# docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
# ubuntu 컨테이너의 현재 상태를 my_ubuntu:v1 이미지로 생성
docker commit -a app -m "first commit" ubuntu my_ubuntu:v1
```

### Dockerfile을 기반으로 이미지 생성
```Dockerfile
FROM node:12-alpine
RUN apk add --no-cache python3 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

```shell
# ./ 디렉토리를 빌드 컨텍스트로 
docker build -t my_app:v1 ./
# ./ 디렉토리를 빌드 컨텍스트로, example/MyDockerfile 사용
docker build -t my_app:v1 -f example/MyDockerfile ./
```

- 빌드 컨텍스트
    - 도커 빌드 명령 수행 시 현재 디렉토리를 빌드 컨텍스트라 함
    - Dockerfile로부터 이미지 빌드에 필요한 정보를 도커 데몬에 전달
- `.dockerignore` 
    - `.gitignore`와 같은 문법
    - 특정 디렉토리 혹은 파일 목록을 빌드 컨텍스트에서 제외


## Dockerfile 문법
- [도커 파일 공식문서](https://docs.docker.com/reference/dockerfile/)


