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

