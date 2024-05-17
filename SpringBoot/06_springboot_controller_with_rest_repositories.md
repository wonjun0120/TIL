# Rest Repository로 만드는 Controller, HAL Explorer
Rest Repository와 Rest Repository HAL Explorer를 사용하여 레포지토리에서 바로 컨트롤러 생성하는 방법에 대해 정리

## Rest Repository 의존성
- `Repository`의 내용을 바로 `Controller`로 내보내는 의존성
- `application.properties` 파일에서 `base-path` 설정 가능
- `application.properties` 파일에서 `detection-strategy`의 값을 변경하여 어떤 Repository를 Rest API로 내보낼지 결정 가능
    - `DEFAULT`     : 기본
    - `ALL`         : 모든 Repository 내보내기
    - `ANNOTATED`   : `@RepositoryRestResource` 어노테이션으로 표기한 Repository만 Rest API로 내보내기
    - `VISIBILITY`  : Public 접근자로 설정된 Repository만 Rest API로 내보내기

## Rest Repository HAL Explorer 의존성
- Rest API HAL Explorer를 보여주는 의존성
- HAL 및 HAL-FORMS 기반 HTTP 응답을 쉽게 탐색할 수 있는 Angular 기반 웹 애플리케이션

### JSON HAL
- HAL은 API의 리소스들 사이에 쉽고 일관적인 하이퍼링크를 제공하는 방식이다. API 설계시 HAL을 도입하면 API간에 쉽게 검색이 가능하다. 따라서 해당 API를 사용하는 다른 개발자들에게 좀 더 나은 개발 경험을 제공한다.
- Response 메시지에 부가적인 메타 정보들도 담아 연관된 다른 API를 손쉽게 사용할 수 있게끔 설계

```text
self 링크로 표현되는 ('/orders')를 대표하는 메인 리소스의 URI
다음 페이지의 순서를 가르키는 next 링크
'ea:find'에 호출되어 아이디로 순서를 검색하는 templated 링크
배열에 저장된 여러개의 'ea:admin'링크 오브젝트들
orders 컬렉션의 두개의 프로퍼티; 'currentlyProcessing'과 'shippedToday'
프로퍼티와 그 자체 링크를 포함한 Embbeded order 리소스
API의 다큐멘테이션 URL로 링크로 확장하기 위한 'ea'로 명시된 압축 URI
```


# 참고자료
패스트캠퍼스 - 10개 프로젝트로 완성하는 백엔드 웹개발 (Java/Spring) 초격차 패키지

[공식문서 - Spring Data Rest The HAL Explorer](https://docs.spring.io/spring-data/rest/reference/tools.html)

[블로그 - REST API에 HAL(Hypertext Application Language) 적용하기 by Justin Yoo](https://blog.aliencube.org/ko/2015/08/16/applying-hal-to-rest-api/)

[블로그 - \[번역\] HAL - Hypertext Application Language by peter park](https://velog.io/@pop8682/%EB%B2%88%EC%97%AD-HAL-Hypertext-Application-Language)