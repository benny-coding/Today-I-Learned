## 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기
  - 스프링 시큐리티(Spring Security)는 막강한 인증(Authentication)과
    인가(Authorization)(혹은 권한 부여) 기능을 가진 프레임워크이다.
  - 스프링 기반의 애플리케이션에서는 보안을 위한 표준이다.
  - 인터셉터, 필터 기반의 보안 기능을 구현하는 것보다 스프링 시큐리티를 통해
    구현하는 것을 적극적으로 권장하고 있음

  ### 스프링 시큐리티와 스프링 시큐리티 Oauth2 클라이언트
    - 많은 서비스들은 로그인 기능을 id/password 방식보다 소셜 로그인을 많이 사용한다.
    - 이유는 직접 구현할 경우 배보다 배꼽이 커진다. (다음과 같은 것들을 직접 구현해야 한다.)
      - 로그인 시 보안
      - 회원가입 시 이메일 혹은 전화번호 인증
      - 비밀번호 찾기
      - 비밀번호 변경
      - 회원정보 변경
    - 스프링 부트 1.5 vs 스프링 부트 2.0
      - 연동 방법은 크게 변경되었지만 spring-security-oauth2-autoconfigure
        __라이브러리 덕분에 설정 방법에는 크게 차이가 없는 경우를 보게 된다.__
    - spring-security-oauth2-autoconfigure 라이브러리를 사용할 경우 2.0에서
      1.5의 설정 그대로 사용할 수 있고 __새로운 방법을 쓰기보다는 기존에 안전하게 작동하던 코드__ 를
      사용하는 것이 아무래도 더 확실하므로 많은 개발자가 이 방식을 사용해 왔다.
    - 하지만 이 책에서는 스프링 부트 2 방식인 Spring Security Oauth2 Client 라이브러리를 사용해서 진행한다.
      - 스프링 팀에서 기존 1.5에서 사용되던 spring-security-oauth 프로젝트는 유지 상태(maintenance mode)로
        결정했으며 더는 신규 기능은 추가하지 않고 버그 수정 정도만 추가될 예정, 신규 기능은 oauth2 라이브러리에서만 지원하겠다고 선언
      - 스프링 부트용 라이브러리(stater) cnftl
      - 기존에 사용되던 방식은 확장 포인트가 적절하게 오픈되어 있지 않아 직접 상속하거나
        오버라이딩 해야 하고 신규 라이브러리의 경우 확장 포인트를 고려해서 설계된 상태
    - 스프링 부트 2 방식의 자료를 찾고 싶은 경우 인터넷 자료들 사이에서 다음 두 가지만 확인하면 된다.
      - 먼저 __spring-security-oauth2-autoconfigure 라이브러리__ 를 썼는지 확인
      - `application.properties` 혹은 `application.yml` 정보의 양의 차이가 있는지 비교해야한다.
        (Spring Boot 1.5에서 2.x로 넘어오면서 client 인증정보 부분만 입력하면 되게 되었다.)
    - 스프링 부트 1.5 방식은 url 주소를 모두 명시해야 하고 2.0 방식에서는 client 인증 정보만 입력하면 된다.
    - 1.5에서 입력했던 이외의 내용들은 2.0에서 enum으로 대체되었다.
    - __CommonOAuth2Provider__ 라는 enum이 새롭게 추가되어 구글, 깃허브, 페이스북, 옥타(Okta)의 기본 설정값은
      모두 여기서 제공합니다.

  ### 구글 서비스 등록
  1. https://console.cloud.google.com 으로 이동하여 구글 계정으로 로그인 후
    `프로젝트 선택` 탭을 클릭한다.
  2. 프로젝트 선택 팝업에서 `새 프로젝트` 버튼을 누른다.
  3. `프로젝트 이름`에 프로젝트의 이름을 예제대로로 freelec-springboot2-webservice로 입력한다
  4. 좌측 메뉴에서 API 및 서비스 메뉴에 들어간다.
  5. 사용자 인증 정보 메뉴에 들어가서 만들 프로젝트를 선택한다. 
  6. [사용자 인증 정보 만들기] 버튼을 클릭한다.
  7. OAuth 클라이언트 ID를 클릭한다.
  8. OAuth 클라이언트 ID 만들기에서 [동의 화면 구성] 버튼을 클릭한다.
  9. User Type에서 외부를 선택한 후 [만들기] 버튼을 클릭 한다.
  10. OAuth 동의 화면 입력 내용 설명
    - __애플리케이션 이름__ : 구글 로그인 시 사용자에게 노출될 애플리케이션 이름을 이야기합니다.
    - __지원 이메일__ : 사용자 동의 화면에서 노출될 이메일 주소입니다. 보통은 서비스의 help 이메일 주소를
      사용하지만, 여기서는 독자의 이메일 주소를 사용하시면 됩니다.
    - __Google API의 범위__ : 이번에 등록할 구글 서비스에서 사용할 범위 목록입니다. 기본값은 
      email/profile/openid이며, 여기서는 딱 기본 범위만 사용합니다. 이외 다른 정보들도 사용하고 싶다면 
      범위 추가 버튼으로 추가하면 됩니다.
  11. OAuth 클라이언트 ID 만들기에서 [웹 애플리케이션]을 선택하고 이름을 입력합니다.
  12. 하단에 승인된 리디렉션 URI에 `http://localhost:8080/login/oauth2/code/google`을 입력 후
      [생성] 버튼클 클릭한다.
  13. 승인된 리디렉션 URI 설명
    - 서비스에서 파라미터로 인증 정보를 주었을 때 인증이 성공하면 구글에서 리다이렉트할 URL입니다.
    - 스프링 부트 2 버전의 시큐리티에서는 기본적으로 `{도메인}/login/oauth2/code/{소셜서비스}`로
      리다이렉트 URL을 지원하고 있습니다.
    - 사용자가 별도로 리다이렉트 URL을 지원하는 Controller를 만들 필요가 없습니다.
      시큐리티에서 이미 구현해 놓은 상태입니다.
    - 현재는 개발 단계이므로 http://localhost:8080/login/oauth2/code/google로만 등록합니다.
    - AWS 서버에 배포하게 되면 localhost 외에 추가로 주소를 추가해야하며, 이건 이후 단계에서 진행하겠습니다.
  14. 생성이 완료되면 클라이언트 ID와 클라이언트 보안 비밀을 확인할 수 있다.
  15. `src/main/resources/` 디렉토리에 `application-oauth.properties` 파일을 생성한다.
  16. 클라이언트 ID와 클라이언트 보안 비밀 코드를 등록한다.
  17. scope는 기본으로 openid,profile,email이고 profile과 email만 등록하는 이유는 
      openid 등록 시 open id provider(제공자)로 인식을 하여 provider인 서비스와 그렇지 않은 서비스를
      나누어 각각 OAuth2Service를 만들어야 한다.
      그러므로 하나의 OAuth2Service로 사용하기 위해 일부러 openid scope를 빼고 등록한다.
    - 스프링 부트에서는 properties의 이름을 application-xxx.properties로 만들면
      xxx라는 이름의 profile이 생성되어 이를 통해 관리할 수 있다.
      즉, profile=xxx라는 식으로 호출하면 __해당 properties의 설정들을 가져올 수 있다.__
      호출하는 방식은 여러 방식이 있지만 스프링 부트의 기본 설정 파일인 application.properties에서
      application-oauth.properties를 포함하도록 구성합니다.
  ### 구글 로그인 연동하기
    - __@Enumerated(EnumType.STRING)__
      - JPA로 데이터베이스로 저장할 때 Enum 값을 어떤 형태로 저장할지를 결정합니다.
      - 기본적으로 int로 된 숫자가 저장됩니다.
      - 숫자로 저장되면 데이터베이스로 확인할 때 그 값이 무슨 코드를 의미하는지 알 수가 없습니다.
      - 그래서 문자열(EnumType.STRING)로 저장될 수 있도록 선언합니다.
    - __findByEmail__
      - 소셜 로그인으로 반환되는 값 중 email을 통해 이미 생성된 사용자인지 처음 가입하는 사용자인지
        판단하기 위한 메소드입니다.
    - 스프링 시큐리티 설정
      1. `build.gradle`에 스프링 시큐리티 관련 의존성을 추가한다.
      - __spring-boot-starter-oauth2-client__
        - 소셜 로그인 등 클라이언트 입장에서 소셜 기능 구현 시 필요한 의존성입니다.
        - spring-security-oauth2-client와 spring-security-oauth2-jose를 기본으로 관리해준다.
      - config.auth 패키지는 __시큐리티 관련 클래스가 담긴다.__
    - __@EnableWebSecurity__
      - Spring Security 설정들을 활성화시켜 줍니다.
    - __csrf( ).disable( ).headers( ).frameOptions( ).disable( )__
      - h2-console 화면을 사용하기 위해 해당 옵션들을 disable 합니다.
    - __authorizeRequests__
      - URL별 권한 관리를 설정하는 옵션의 시작점입니다.
      - authorizeRequests가 선언되어야만 antMatchers 옵션을 사용할 수 있습니다.
    - __antMatchers__
      - 권한 관리 대상을 지정하는 옵션입니다.
      - URL, HTTP 메소드별로 관리가 가능합니다.
      - "/"등 지정된 URL들은 permitAll( ) 옵션을 통해 전체 열람 권한을 주었습니다.
      - POST 메소드이면서 "/api/v1/**" 주소를 가진 API는 USER 권한을 가진 사람만 가능하도록 했습니다.
    - __anyRequest__
      - 설정된 값들 이외 나머지 URL들을 나타냅니다.
      - 여기서는 authenticated()을 추가하여 나머지 URL들은 모두 인증된 사용자들에게만 허용하게 합니다.
      - 인증된 사용자 즉, 로그인한 사용자들을 이야기합니다.
    - __logout( ).logoutSuccessUrl("/")__
      - 로그아웃 기능에 대한 여러 설정의 진입점입니다.
      - 로그아웃 성공 시 /주소로 이동합니다.
    - __oauth2Login__
      - OAuth2 로그인 기능에 대한 여러 설정의 진입점입니다.
    - __userInfoEndPoint__
      - OAuth2 로그인 성공 이후 사용자 정보를 가져올 때의 설정들을 담당합니다.
    - __userService__
      - 소셜 로그인 성공 시 후속 조치를 진행할 UserService 인터페이스의 구현체를 등록합니다.
      - 리소스 서버(즉,소셜 서비스들)에서 사용자 정보를 가져온 상태에서 추가로 진행하고자 하는 기능을
        명시할 수 있습니다.