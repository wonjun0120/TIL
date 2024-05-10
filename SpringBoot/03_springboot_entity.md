# 스프링부트 엔티티
spring web layer에서 Domain Model 계층중 하나인 @Entity에 대해서 정리

## @Entity 사용 예시
```java
@Getter
@ToString
@Table(indexes = {
        @Index(columnList = "title"),
        @Index(columnList = "hashtag"),
        @Index(columnList = "createdAt"),
        @Index(columnList = "createdBy")
})
@EntityListeners(AuditingEntityListener.class) //JPA Auditing
@Entity
public class Article {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    // 컬럼별 Setter 생성, Column 어노테이션을 통해 notnull, length 설정
    @Setter @Column(nullable = false) private String title; 
    @Setter @Column(nullable = false, length = 10000) private String content; 

    @Setter private String hashtag;

    @ToString.Exclude   // ToString 제외 
    @OrderBy("id")     
    @OneToMany(mappedBy = "article", cascade = CascadeType.ALL) //일대 다 관계
    private final Set<ArticleComment> articleComments = new LinkedHashSet<>();

    // JPA Auditing, 자동 생성
    @CreatedDate @Column(nullable = false) private LocalDateTime createdAt; // 생성일시
    @CreatedBy @Column(nullable = false, length = 100) private String createdBy; // 생성자
    @LastModifiedDate @Column(nullable = false) private LocalDateTime modifiedAt; // 수정일시
    @LastModifiedBy @Column(nullable = false, length = 100) private String modifiedBy; // 수정자


    protected Article() {} // @Entity 선언시 기본 생성자 선언 필요, public, protected 접근제어가능

    // 실제 사용 생성자, 외부 생성 방지를 위해 private로 선언
    private Article(String title, String content, String hashtag) {
        this.title = title;
        this.content = content;
        this.hashtag = hashtag;
    }

    // 정적 팩토리 메소드
    public static Article of(String title, String content, String hashtag) {
        return new Article(title, content, hashtag);
    }

    // Equals and Hash Code
    // 객체가 서로 같은지 판별, Entity는 Id값이 같으면 서로 같은 객체이기에 맞춰 설정
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Article article)) return false;
        return id != null && id.equals(article.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }

}
```

## @Entity에서 NoArgsConstructor가 필요한 이유
- JPA Provider가 도메인 객체를 동적으로 인스턴스화해야하는 경우가 종종 있고, 인수가 없는 기본 생성자가 있어야 이 동작이 가능하기 때문 (StackOverFlow)
- JPA 지연로딩, 추후 추가 정리


## 정적 팩토리 메소드
- GoF 디자인 패턴 중 팩토리 패턴에서 유래
- 객체를 생성하는 역할을 분리
- 객체를 new 키워를 사용하여 생성자로 생성하는 경우, 클래스의 구조를 잘 알고 있어야 생성이 가능, 이 점을 개선하기 위해 어떤 인수를 받아야 객체를 생성할 수 있는지 정적 팩토리 메소드를 통해 명시 가능.
- 또 이름을 설정하여, 상황에 맞는 생성자 사용을 통해 사용성을 높일 수 있음
- 생성자에 들어갈 인수를 정적 팩토리 메소드를 통해 걸러낼 수 있음

### 정적 팩토리 메서드 네이밍 컨벤션
- from : 하나의 매개 변수를 받아서 객체를 생성
- of : 여러개의 매개 변수를 받아서 객체를 생성
- getInstance | instance : 인스턴스를 생성. 이전에 반환했던 것과 같을 수 있음.
- newInstance | create : 새로운 인스턴스를 생성
- get[OtherType] : 다른 타입의 인스턴스를 생성. 이전에 반환했던 것과 같을 수 있음.
- new[OtherType] : 다른 타입의 새로운 인스턴스를 생성.

# 참고자료
패스트캠퍼스 - 10개 프로젝트로 완성하는 백엔드 웹개발 (Java/Spring) 초격차 패키지

[StackOverFlow - Why does JPA require a no-arg constructor for domain objects?](https://stackoverflow.com/questions/2808747/why-does-jpa-require-a-no-arg-constructor-for-domain-objects)

[블로그 - JPA Entity의 기본 생성자 관련 예외 정리하기 - wbluke](https://wbluke.tistory.com/6)

[블로그 - 정적 팩토리 메소드는 왜 사용할까? - ](https://tecoble.techcourse.co.kr/post/2020-05-26-static-factory-method/)