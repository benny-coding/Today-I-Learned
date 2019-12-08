## 테스트 코드 작성 해보기
  - Java 디렉토리 밑으로 패키지를 하나 생성한다.
  - 클래스 파일을 하나 생성한다.
  - 패키지 가져오기는 `Option + Enter` 버튼을 한다
  - `@SpringBootApplication`은 스프링 부트의 자동 설정, 스프링 Bean 읽기와 생성을 모두 자동으로 설정한다.
  - `@SpringBootApplication`의 위치부터 설정을 읽어나가기 시작하며 이 클래스는 항상 프로젝트의 최상단에 위치해야 한다.
  - main 메소드에서 실행하는 `SpringApplication.run`으로 인해 내장 WAS를 실행합니다.
  - 내장 WAS란 별도로 외부에 WAS를 두지 않고 애플리케이션을 실행할 때 내부에서 WAS를 실행하는 것을 이야기하며 
    __서버에 톰캣을 설치할 필요가 없고__ , 스프링 부트로 만들어진 `Jar` 파일로 실행하면 된다.
  - Jar 파일이란 실행 가능한 Java 패키징 파일이다.
  - 스프링 부트에서는 __내장 AWS를 사용하는 것을 권장__ 하고 있으며 이유는 __언제 어디서나 같은 환경에서 스프링 부트를 배포__ 할 수 있기 때문이다.
  - __@RestController__
    - 컨트롤러를 JSON으로 반환하는 컨트롤러로 만들어 줍니다.
    - 예전에는 `@ResponseBody`를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게
      해준다고 생각하면 됩니다.
  - __@GetMapping__
    - HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 줍니다.
    - 예전에는 `@RequestMapping(method= RequestMethod.GET)`으로 사용되었으나 이제는 
      `/hello`로 요청이 오면 문자열 hello를 반환하는 기능을 가지게 되었습니다.
  - 테스트 코드로 검증하기 위해서 `src/test/java` 경로로 `src/main/java`의 패키지를 그대로 생성한다.
  - 테스트 클래스는 대상 클래스 이름 뒤에 TEST를 붙인다. ex) HelloControllerTest
  - __@RunWith(SpringRunner.class)__
    - 테스트 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킵니다.
    - 여기서는 SpringRunner라는 스프링 실행자를 사용합니다
    - 즉, 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 합니다.
  - __@WebMvcTest__
    - 여러 스프링 테스트 어노테이션 중, Web(Spring MVC)에 집중할 수 있는 어노테이션입니다.
    - 선언할 경우 `@Controller`, `@ControllerAdvice`를 사용할 수 있습니다.
    - 단, `@Service`, `@Component`, `@Repository` 등은 사용할 수 없습니다.
    - 여기서는 컨트롤러만 사용하기 때문에 선언합니다.
  - __@Autowired__
    - 스프링이 관리하는 빈(Bean)을 주입 받습니다.
  - __private MockMvc mvc__
    - 웹 API를 테스트할 때 사용합니다.
    - 스프링 MVC 테스트의 시작점입니다.
    - 이 클래스를 통해 HTTP GET, POST 등에 대한 API 테스트를 할 수 있습니다.
  - __mvc.perform(get("/hello"))__
    - MockMvc를 통해 /hello 주소로 HTTP GET 요청을 합니다.
    - 체이닝이 지원되어 아래와 같이 여러 검증 기능을 이어서 선언할 수 있습니다.
  - __.andExpect(status().isOk())__
    - mvc.perform의 결과를 검증합니다.
    - HTTP Header의 Status를 검증합니다.
    - 우리가 흔히 알고 있는 200,404,500 등의 상태를 검증합니다.
    - 여기선 OK 즉, 200인지 아닌지를 검증합니다.
  - __.andExpect(content().string(hello))__
    - mvc.perform의 결과를 검증합니다.
    - 응답 본문의 내용을 검증합니다.
    - Controller에서 "hello"를 리턴하기 때문에 이 값이 맞는지 검증합니다.
  - 테스트는 메서드 좌측 화살표 클릭으로 실행한다.
  - __절대로 수동으로 검증하고 테스트 코드를 작성하지 않는다.__

## 롬복 소개 및 설치하기
  - `롬복(Lombok)`은 자바 개발자들의 필수 라이브러리이다.
  - 이클립스는 설치가 번거롭지만 인텔리제이는 플러그인으로 쉽게 설치가 가능하다. 
  - `build.gradle`에 `compile('org.projectlombok:lombok')`을 추가한다.
  - `Command + Shift + A`로 action으로 가서 Plugins를 실행한다.
  - `Lombok`을 검색하여 INSTALL 후 인텔리제이를 재시작한다.
  - `Setting > Build > Compiler > Annotation Processors`를 들어가서 
    `Enable annotation processing`을 체크한다.
  - Lombok은 프로젝트마다 설정할 수 있다.

## Hello Controller 코드 롬복으로 전환
  - __@Getter__
    - 선언된 모든 필드의 get 메소드를 생성해 줍니다.
  - __@RequiredArgsConstructor__
    - 선언된 모든 final 필드가 포함된 생성자를 생성해 줍니다.
    - final이 없는 필드는 생성자에 포함되지 않습니다.
  - __asertTaht__
    - `assertj`라는 테스트 검증 라이브러리의 검증 메소드입니다.
    - 검증하고 싶은 대상을 메소드 인자로 받습니다.
    - 메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용할 수 있습니다.
  - __isEqualTo__
    - assertj의 동등 비교 메소드입니다.
    - assertThat에 있는 값과 isEqualTo의 값을 비교해서 같은 때만 성공입니다.
