## 스프링 부트에서 JPA로 데이터베이스 다뤄보자
  - 실제로 실행된 쿼리는 어떤 형태일까?
    - `src/main/sesources` 디렉토리 아래에 `application.properties` 파일을 생성한다.

## 등록/수정/조회 API 만들기
  - API를 만들기 위해서는 총 3개의 클래스가 필요하다
    1. Request 데이터를 받을 Dto
    2. API 요청을 받을 Controller
    3. 트랜잭션, 도메인 기능 간의 순서를 보장하는 Service
       (__Service는 비지니스 로직을 처리하는 것이 아닌 트랜잭션, 도메인 간 순서 보장의 역할을 한다.__)

  - Spring 웹 계층
    - Web Layer
      - 흔히 사용되는 컨트롤러(@Controller)와 JSP/Freemarker 등의 뷰 템플릿 영역입니다.
      - 이외에도 필터(@Filter), 인터셉터, 컨트롤러 어드바이스(@ControllerAdvice) 등 
        __외부 요청과 응답__ 에 대한 전반적인 영역을 이야기합니다.
    - Service Layer
      - @Service에 사용되는 서비스 영역입니다.
      - 일반적으로 Controller와 Dao의 중간 영역에서 사용됩니다.
      - @Transaction이 사용되어야 하는 영역이기도 합니다.
    - Repository Layer
      - __DataBase__ 와 같이 데이터 저장소에 접근하는 영역입니다.
      - 기존에 개발하셨던 분들이라면 Dao(Data Access Object) 영역으로 이해하시면 쉬울 것입니다.
    - Dtos
      - Dto(Data Transfer Object)는 __계층 간에 데이터 교환을 위한 객체__ 를 이야기하며 Data는
        이들의 영역을 얘기합니다.
      - 예를 들어 뷰 템플릿 엔진에서 사용될 객체나 Repository Layer에서 
         결과로 넘겨준 객체 등이 이들을 이야기합니다.
    - Domain Model
      - 도메인이라 불리는 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 있고 공유할 수 있도록
        단순화시킨 것을 도메인 모델이라고 합니다.
      - 이를테면 택시 앱이라고 하면 배차, 탑승, 요금 등이 모두 도메인이 될 수 있습니다.
      - @Entity를 사용해보신 분들은 @Entity가 사용된 영역 역시 도메인 모델이라고
        이해 해주시면 됩니다.
      - 다만, 무조건 데이터베이스의 테이블과 관계가 있어야만 하는 것은 아닙니다
      - VO처럼 값 객체들도 이 영역에 해당하기 때문입니다.
    - 위 5가지 레이어 중 비지니스 처리를 담당해야 할 곳은 Domain이며
      기존에 서비스로 처리하던 방식은 __트랜잭션 스크립트__ 라고 한다.
    - 모든 로직이 __서비스 클래스 내부에서 처리되는__ 트랜잭션 스크립트는
      __서비스 계층이 무의미하며, 객체란 단순히 데이터 덩어리__ 역할만 하게 됩니다.
    - 도메인 모델에서 처리할 경우 order, billing, delivery가 각자 본인의 취소 이벤트를 처리를 하며,
      서비스 메소드는 __트랜잭션과 도메인 간의 순서만 보장__ 해 줍니다.
    
    - 스프링에서 Bean을 주입받는 방식들
      - @Autowired
      - setter
      - 생성자
    - @RequiredArgsConstructor
      - 위 방식들 중에서 권장하는 방식은 @RequiredArgsConstructor를 통해 생성자로 주입받는 방식이다.
      - @RequiredArgsConstructor는 final이 선언된 모든 필드를 인자값으로 하는 생성자를 생성해준다.
      - 컨트롤러에서 새로운 서비스를 추가하거나 기존 컴포넌트를 제거하는 이슈가 발생해도 생성자에는 손을 대지 않아도 된다.
    - __Entity 클래스를 Request/Response 클래스로 사용해서는 안된다.__
    - Entity 클래스는 __데이터베이스와 맞닿은 핵심 클래스__ 입니다.
