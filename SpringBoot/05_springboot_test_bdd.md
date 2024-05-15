# 스프링부트 테스트, Given-When-Then
스프링부트 테스트 코드에 대한 정리

## Test 예시 - Given When Then
```java
@DisplayName("전체 테스트")
class ArticleRepositoryTest {
    @Autowired private ArticleRepository articleRepository;

    @DisplayName("세부 테스트")
    @Test
    void given_when_then() {
        // Given

        // When

        // Then

    }
}
```

### Given When Then, BDD 스타일 어센션
- Given : 테스트 준비 단계, 사용하는 변수 지정
- When : 실제 엑션 테스트 단계
- Then : 테스트 검증 단계
- BDD : 행위 주도 개발, Behavior-driven development

## Junit, AssertJ 비교
- AssertJ는 더 많은 Assert 문을 제공하여 가독성 증가와 편의 증가, 메서드 체이닝 제공
- [Junit](https://junit.org/junit5/docs/current/user-guide/) 문서, 문서에서도 AssertJ 사용 권장

# 참고자료
패스트캠퍼스 - 10개 프로젝트로 완성하는 백엔드 웹개발 (Java/Spring) 초격차 패키지

[블로그 - [SPRING TEST] Given-When-Then 패턴 by choi in ho](https://velog.io/@rising_developer/SPRING-TEST-Given-When-Then-%ED%8C%A8%ED%84%B4)