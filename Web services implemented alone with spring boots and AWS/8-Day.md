## 등록/수정/조회 API 만들기
  - Entity 클래스를 기준으로 테이블이 생성되고 스키마가 변경되는데
    화면 변경은 아주 사소한 기능인데 이를 위해 테이블과 연결된 Entity 클래스를 변경하는 것은 너무 큰 변경이다.
    때문에 View Layer와 DB Layer의 역할 분리는 철저하게 하는 것이 좋으며,
    실제로 Controller에서 __결괏값으로 여러 테이블을 조인해서 주어야 할 경우__ 가 빈번하여
    Entity 클래스만으로 표현이 어려운 경우가 많아 꼭 Entity 클래스와 Controller의 Dto를 분리해서
    사용할 줄 알아야 한다.
  - @WebMvcTest는 JPA 기능이 작동하지 않고 ControllerAdvice 등 외부 연동과 관련된 부분만 활성화된다.
    그러므로 JPA 기능까지 테스트 시에는 @SpringBootTest와 TestRestTemplate을 사용하면 된다.
  - __WebEnvironement.RANDOM_PORT__ 사용 시 랜던 포트가 실행되고 insert 쿼리가 실행되었다.

  - PostsResponseDto는 __Entity의 필드 중 일부만 사용__ 하므로 생성자로 Entity를 받아 필드에 값을 넣는다.
    이처럼 모든 필드를 가진 생성자가 필요하진 않을 때 Dto는 entity를 받아 처리한다.
  ### JPA의 영속성 컨텍스트
  - __Entity를 영구 저장하는 환경__ 이다.
  - 일종의 논리적 개념이며, JPA의 핵심 내용은 엔티티가 영속성 컨텍스트에
    포함되어 있냐 아니냐로 갈린다.
  - JPA의 엔티티 매니저는 Spring Data Jpa를 쓴다면 기본으로 활성화 되는데 이 상태로
    __트랜잭션 안에서 데이터베이스의 데이터를 가져오면__ 이 데이터는 영속성 컨텍스트가 유지된 상태이다.
  - 이 상태에서 데이터의 값을 변경하면 __트랜잭션이 끝나는 시점에 해당 테이블에 변경분을 반영__ 합니다.
    즉, Entity 객체의 값만 변경하면 별도로 __Update 쿼리를 날릴 필요가 없다.__
    이 개념을 __더티 체킹(dirty checking)__ 이라고 한다.
  - JPA 사용시 SQL 맵퍼를 사용했을 때보다 좀 더 객체지향적으로 코드가 변했음을 알 수 있다.

  ### 조회 기능 실제로 톰캣에서 실행해서 확인해보기
  - 로컬 환경에서 H2를 사용하여 웹 콘솔 환경에서 확인해볼 수 있다.
    ```java
    spring.h2.console.enabled=true
    ```
    위 내용을 application.properites에 추가한다.
    그 후 Application 클래스의 main 메소드를 실행한 후 localhost:8080/h2-console로 접속하면 웹 콘솔 화면을 볼 수 있다.
  - 크롬에서 JSON Viewer라는 플러그인을 설치하면 Json 데이터를 가독성 있게 볼 수 있다.
  ### JPA Auditing의 사용
  - 날짜 타입은 LocalDate와 LocalDateTime이 등장했고 이는 기존 Date의 문제점을 고친 타입으로 무조건 사용하는 것이 좋다.
  - __@MappedSuperclass__
    - JPA Entity 클래스들이 BaseTimeEntity를 상속할 경우 필드들(createdDate, modifiedDate)도
      칼럼으로 인식하도록 합니다.
  - __@EntityListeners(AuditingEntityListener.class)__
    - BaseTimeEntity 클래스에 Auditing 기능을 포함시킵니다.
  - __@CreatedDate__
    - Entity가 생성되어 저장될 때 시간이 자동 저장됩니다.
  - __@LastModifiedDate__
    - 조회한 Entity의 값을 변경할 때 시간이 자동 저장됩니다.
  - JPA Auditing 어노테이션들을 모두 활성화하려면 Application 클래스에 활성화 어노테이션 하나를 추가한다.

  ## 머스테치로 화면 구성하기
    ### 서버 템플릿 엔진과 머스테치 소개
      - 서버 템플릿 엔진이란?
        - __지정된 템플릿 양식과 데이터__ 가 합쳐서 HTML 문서를 출력하는 소프트웨어를 이야기합니다.
        - JSP, Freemarker는 서버 템플릿 엔진, 리액트와 뷰는 클라이언트 템플릿 엔진이다.
      - 서버 템플릿 엔진을 이용한 화면 생성은 서버에서 Java 코드로 문자열을 만든 뒤 이 문자열을
        HTML로 변환하여 브라우저로 전달합니다.
      - 자바스크립트는 브라우저 위에서 작동하며 코드가 실행되는 장소는 서버가 아닌 브라우저이다.
      - Vue.js나 React.js를 이용한 SPA는 브라우저에서 화면을 생성한다. 즉 서버에서 이미 코드가 벗어난 경우이다.
      - 머스테치는 커뮤니티 버전을 사용해도 플러그인을 사용할 수 있다.
    ### 기본 페이지 만들기
      - `build.gradle`에 compile('org.springframework.boot:spring-boot-starter-mustache') 추가한다
      - 머스테치는 __스프링 부트에서 공식지원하는 템플릿 엔진__ 이다.
      - 파일 위치는 기본적으로 src/main/resources/templates 이다.