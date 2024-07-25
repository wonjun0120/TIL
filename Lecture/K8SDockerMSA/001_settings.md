# kubectl, kustomize, minikube

## kubectl
- 쿠버네티스의 API서버와 통신하여 사용자 명령 전달할 수 있는 CLI도구

```shell
brew install kubectl
```

### kubectl에서 k8s클러스터와 통신하기 위한 설정
- 파일 보기
```shell
vi ~/.kube/config
```
- 연결할 클러스터를 등록하여 사용 가능
- cluster: 연결할 클러스터들을 여러개 정의하여 사용 가능, 접속할 클러스터 정보
- context : 클러스터와 유저 조합, 어떤 클러스터에서 어떤 유저로 접속할건지 정의
- users : 인증사용자 정보

- 접속정보
```shell
kubectl get nodes
kubectl cluster-info
```

## kustomize
- 쿠버네티스의 매니페스트 파일 효율적으로 관리할 수 있게 도와주는 도구
    - 각 환경별로 파일 관리 가능
- 양대산맥 Helm - chart
    - 패키지 기반 관리

```shell
brew install kustomize
```

## minikube
- 가상환경을 사용하여 쿠버네티스 클러스터 구현
- 원하는 가상환경 선택 가능, docker에서 진행
- 학습 목적으로 활용

### 기본 사용법
``` shell
minikube start --driver docker  # 실행, 도커에서
minikube status                 # 상태확인
minikube stop                   # 중지
minikube delete                 # 삭제
minikube pause                  # 일시중지
minikube unpause                # 재개
minikube addons list            # 애드온 목록 확인
minikube addons enable [addon]  # 애드온 활성화 
minikube addons disable [addon] # 애드온 비활성화
minikube ssh                    # 클러스터 노드에 SSH 접속
minikube kubectl                # 쿠버네티스 클러스터 버전과 대응되는 kubectl사용
```

- minikube addons
    - 실제 쿠버네티스에서는 지원하지 않음
    - nginx ingress, helm과 같은 애드온 사용가능

# Terraform
- [예제코드](https://github.com/tedilabs/fastcampus-devops/tree/main/3-docker-kubernetes/env/terraform-aws-ubuntu)