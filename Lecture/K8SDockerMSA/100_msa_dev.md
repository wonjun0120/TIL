# MSA 개발 방법

## MSA 특징
- 빠르게 개발해 지속적으로 배포
- 수동 혹은 자동으로 쉽게 스케일링
- 마이크로서비스는 데이터베이스와 데이터를 공유하지 않음
- 명확한 인터페이스를 통해서만 통신
- 개별적인 런타임 프로세스로 배포
- 마이크로서비스 인스턴스는 상태가 없음
- 개발자가 작성 할 수 있을 만한 크기로 구현
- 성능이나 데이터 일관성을 저해하지 않을 정도의 규모

## MSA 문제점
- 동기식 통신을 사용하는 다수의 소형 컴포넌트는 연쇄 장애 발생 가능
- 다수의 소형 컴포넌트를 최신 상태로 유지하는 것이 어려움
- 많은 컴포넌트 처리에 관여하는 요청은 추적하기 어려움
- 컴포넌트 수준의 하드웨어 지원 사용량 분석 어려움
- 다수의 소형 컴포넌트를 수동으로 구성하고 관리할 때 비용이 많이 들고 오류 발생 쉬움

## MSA 디자인 패턴 목록
- 서비스 디스커버리
    - 마이크로서비스를 자동으로 등록 및 해지
    - 요청을 마이크로서비스 엔드포인트에 보내면 여러개 중 1개로 라우팅
- Edge 서버
    - 외부 마이크로서비스로만 연결, 내부 서비스는 외부에 공개되지 않음
    - 외부로 공개시 표준 프로토콜 및 OAuth, API Key 등 보안 적용 후 연결
- Reactive 마이크로서비스
    - 비동기 형태로 메시지 처리
    - 동기식 형태로 처리가 요구되면 논블로킹 I/O 사용
- Config 중앙화
    - 마이크로서비스의 설정 정보를 중앙서버에 저장/관리
- Logging 중앙화
    - 로그 이벤트 수집 및 처리 후 검색 가능하도록 중앙서버에서 저장/관리
    - 로그 이벤트를 조회 및 분석하기 위한 API / GUI 제공
- Distributed Tracing 
    - 모든 요청 및 메시지 고유 ID가 있고, 로그 이벤트에도 ID 적용
    - 사전에 정의된 ID가 적용되고 로그 이벤트에서 ID로 검색 및 분산 추적
- Circuit Breaker 
    - 대상 서비스 문제를 감지하면, 새로운 요청을 보내지 않도록 차단
    - Circuit을 Open 후 장애 확산을 방지하고, 조치가 완료되면 Close로 원복
- Control loop
    - 원하는 상태와 현재 상태를 비교, 관찰
    - 두 상태가 다른 경우에는 GitOps 기반으로 상태를 일치하도록 Sync 수행
- Monitoring & Alarm 중앙화
    - 자원 사용량의 메트릭 수집 및 새로운 서비스에 대한 메트릭 자동 등록
    - 수집한 메트릭을 조회 및 분석하기 위한 API와 GUI 제공

 