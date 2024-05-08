# 스프링부트 프로젝트 파일 구조
- 스프링부트 프로젝트 파일 구조에 대해서 정리

## MVC 패턴
사용자 인터페이스로부터 비즈니스 로직과 데이터를 분리

자주 변경되는 사용자 인터페이스를 비즈니스 로직과 데이터를 분리하여 유지보수를 더 용이하게 함

- Model
    - 앱이 포함해야할 데이터가 무엇인지 정의
    - 변경이 있을 때 컨트롤러와 뷰에 변경을 알림

- View
    - 앱의 데이터를 사용자에게 보여주는 방식 정의

- Controller
    - 앱의 사용자로부터 입력에 대한 응답으로 모델 및 뷰를 업데이트하는 로직 포함
    - 모델에 명령을 내려 모델의 상태를 변경할 수 있음



## Spring Web Layer

- Web Layer
    - 흔히 사용하는 컨트롤러와 뷰 템플릿 영역
    - 외부 요청과 응답에 대한 전반적인 영역을 이야기

- Service Layer
    - Controller와 Dao의 중간 영역에서 사용
    - @Transaction 사용되어야하는 영역

- Repository Layer
    - Database와 같이 데이터 저장소에 접근하는 영역
    - Dao (Data Access Object)

- DTOs
    - Data Transfer Object
    - 계층간 데이터 교환을 위한 객체

- Domain Model
    - 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 있고, 공유할 수 있도록 단순화시킨 것을 도메인 모델이라함
    - @Entity가 사용된 영역
    - VO 처럼 값 객체들도 이 영역에 해당 
        - VO : Value Object
        - 

# 참고문헌

https://developer.mozilla.org/ko/docs/Glossary/MVC

https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC

[스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 저자: 이동욱](https://product.kyobobook.co.kr/detail/S000001019679)
