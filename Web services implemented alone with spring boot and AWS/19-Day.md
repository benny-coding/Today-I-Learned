## 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기
  ### 어노테이션 기반으로 개선하기
  - __supportsParameter( )__
    - 컨트롤러 메서드의 특정 파라미터를 지원하는지 판단합니다.
    - 여기서는 파라미터에 @LoginUser 어노테이션이 붙어 있고, 파라미터 클래스 타입이
      SessionUser.class인 경우 true을 반환합니다.
  - __resolveArgument( )__
    - 파라미터에 전달할 객체를 생성합니다.
    - 여기서는 세션에서 객체를 가져옵니다.
  - __@LoginUser SessionUser user__
  ### 세션 저장소로 데이터베이스 사용하기
  - 현재까지 개발된 것은 세션을 내장 톰캣 메모리에 저장되고 있다.
  - 세션은 실행되는 Web Application Server의 메모리로 저장이 된다.
    그러므로 톰캣 애플리케이션을 실행 시 항상 초기화되는 구조이다.
  - 2개 이상의 서버에서 서비스하고 있다면 톰캣마다 세션 동기화 설정을 해야만 한다.
  - 현업에서는 세션 저장소에 대해 3가지 중 한가지를 선택한다.
    1. 톰캣 세션을 사용한다.
      - 일반적으로 별다른 설정을 하지 않았을 때 기본적으로 선택되는 방식이다.
      - 이렇게 될 경우 톰캣(WAS)에 세션이 저장되기 때문에 2대 이상의 WAS가 구동되는
        환경에서는 톰캣들 간의 세션 공유를 위한 추가 설정이 필요합니다.
    2. MySQL과 같은 데이터베이스를 세션 저장소로 사용한다.
      - 여러 WAS 간의 공용 세션을 사용할 수 있는 가장 쉬운 방법입니다.
      - 많은 설정이 필요 없지만, 결국 로그인 요청마다 DB IO가 발생하여 성능상 이슈가
        발생할 수 있습니다.
      - 보통 로그인 요청이 많이 없는 백오피스, 사내 시스템 용도에서 사용합니다.
    3. Redis, Mecached와 같은 메모리 DB를 세션 저장소로 사용한다.
      - B2C 서비스에서 가장 많이 사용하는 방식입니다.
      - 실제 서비스로 사용하기 위해서는 Embedded Redis와 같은 방식이 아닌 외부
        메모리 서버가 필요합니다.
    - spring-session-jdbc 등록
      - build.gradle에 `compile('org.springframework.session:spring-session-jdbc')` 등록
      - application.properties에 세션 저장소를 jdbc로 선택하여 코드를 추가한다.
        `spring.session.store-type=jdbc`
      - h2-console로 접속해보면 __JPA로 인해 세션 테이블이 자동 생성되어__ 
        SPRING_SESSION,SPRING_ATTRIBUTES 테이블이 생성되었고 조회 시 세션이 1개 생성되어 있다.
      - 스프링을 재시작시 세션이 풀린다 왜냐하면 H2기반으로 스프링이 재실행될 때 H2도 재시작되기 때문이다.
      - 이후 AWS로 배포하게 되면 AWS의 데이터베이스 서비스인 Relational Database Service(RDS)를 사용하게 되니
        이 때부터는 세션이 풀리지 않는다.


        
