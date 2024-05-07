# 스프링부트 프로젝트 시작하기
- 스프링부트 프로젝트를 처음 세팅하는 방법에 대해 정리합니다.

## 스프링부트란?
- 스프링 프레임워크를 개선한 것
- 개발 환경 설정 간소화, 스타터 프로젝트로 외부 라이브러리 최적화하여 제공
- 웹 애플리케이션 서버 내장, WAS, 톰캣 내장

## 스프링부트 프로젝트 세팅 방법
https://start.spring.io/

- 스프링부트 이니셜라이저를 통해 스프링부트 프로젝트 세팅 가능
- 스프링부트 버전 접미사
    - Snapshot: 현재 테스트중인 단계
    - Mx : 주요 기능 및 버그 수정중인 단계
    - RC : 전반적인 기능과 버그가 모두 수정된 최종 배포 전 단계
    - GA : 최종 배포 단계
    - 접미사가 붙지 않은 버전을 사용하는 것이 좋음
- 스프링 부트 의존성 관리, 자주 사용하는 의존성
    - Spring Web Restful API : RestAPI를 만드는데 필요함
    - H2 Database : 자바로 작성된 인메모리 데이터베이스인 H2
    - Spring Data JPA : 데이터베이스 ORM
    - Lombok : 코드 다이어트 라이브러리, Getter, Setter와 같이 코드의 길이를 줄여주는 라이브러리

## Gitignore 세팅
https://www.toptal.com/developers/gitignore/
- 프로젝트에 맞는 .gitignore 파일을 생성 가능

# 참고자료

[코딩 자율학습 스프링 부트 3 자바 백엔드 개발 입문 - 저자: 홍팍](https://product.kyobobook.co.kr/detail/S000202971420)
