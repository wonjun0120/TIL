# 스프링부트 레포지토리
spring web layer에서 Repository Layer 계층인 Repository에 대해서 정리

## Repository 예시
```java
public interface ArticleRepository extends JpaRepository<Article, Long> {

}
```

## Repository 
- 엔티티에 의해 생성된 데이터베이스 테이블에 접근하는 메서드들을 사용하기 위한 인터페이스
- 각 테이블별 인터페이스 생성하여 사용
- save, findAll, findById

## CrudRepositor와 JpaRepository 차이
- `CrudRepository`는 주로 CRUD 기능을 제공
- `PagingAndSortingRepository`는 페이지 메김 및, 레코드 정렬 기능 제공
- `JpaRepository`는 JPA 특화 기능들, Flush, Crud, PagingAndSorting 등 제공
- CRUD만 필요한 경우, `CrudRepository`사용, Flush 같은 특수한 기능 사용시 `JpaRepository`사용

### Flush?
- 영속성 컨텍스트의 변경 내용을 데이터베이스에 반영

### 영속성 컨텍스트?
- Server side와 Database 사이 엔티티를 저장하는 논리적인 영역
- 1차 캐시, 객체 동일성 보장, Lasy 로딩, 트랜젝션으로 인한 쓰기 지연


# 참고자료
패스트캠퍼스 - 10개 프로젝트로 완성하는 백엔드 웹개발 (Java/Spring) 초격차 패키지


[StackOverFlow - What is difference between CrudRepository and JpaRepository interfaces in Spring Data JPA?](https://stackoverflow.com/questions/14014086/what-is-difference-between-crudrepository-and-jparepository-interfaces-in-spring?answertab=active#tab-top)


[블로그 - 영속성 컨텍스트(Persistence Context) by incheol](https://incheol-jung.gitbook.io/docs/q-and-a/spring/persistence-context)