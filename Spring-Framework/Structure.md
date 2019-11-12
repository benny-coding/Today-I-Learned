## Structure
  * `DispatcherServlet` 은 서버를 처음 실행 시에만 가장 먼저 초기화 된다
  * `DispatcherServlet` 은 `controller` 의 메서드를 호출한다
  * `controller` 의 메서드는 `view` 의 경로를 리턴한다.
  * `"redirect:/경로";` 를 메서드의 `retrun` 으로 사용 시 해당 페이지로 이동한다.
  * `view` 를 나타내는 HTML 파일들은 `resources` 경로에서 특정 위치에 있다.
  * `@GetMapping("경로")` `Annotation` 은 유저가 해당 경로로 들어 왔을 때 실행될 메서드를 연결 시켜준다.
  * `application.properties` 에 데이터베이스 이름, 스키마 경로, 데이터 경로가 정의되어 있다.
  * `db` 는 `resource` 패키지 밑에 위치시킨다.
  * `Bean` 은 `Spring` 가 관리하는 `객체` 를 의미한다.
  * `IoC Container` 는 `BeanFactory` 이고 `ApplicationContext` 는 `BeanFactory` 를 상속 받고 있다.
  * `IoC Container` 의 일은 `Bean` 을 만들고 `의존성` 을 엮어주며 그 `Bean` 들을 제공해준다.
  * `Bean` 으로 등록된 클래스들은 `Intellij` 에서 좌측에 줄번호 옆에 초록색으로 표시 되어 있다.
  * `의존성 주입` 은 `Bean` 끼리만 가능하다. 즉 `IoC Container` 안에 있는 객체 끼리만 의존성이 가능하다.
  * `Spring` 에서의 `Bean` 은 `ApplicationContext` 가 알고 있는 객체이다.
  * `Bean` 을 등록하는 방법은 2가지가 있다.
    * `Component Scanning( @Component )` 
      * `@Repository`
      * `@Servicee`
      * `@Controller`
    * 직접 일일히 `XML` 이나 자바 설정 파일에 `Bean` 으로 등록
  * `Annotation processer` 중 `Spring IoC Container` 가 사용하는 여러가지 `Interface` 가 있다.
    그런 `Interface` 들을 우리는 `LifeCycleCallback` 이라 한다
  * 여러가지 `LifeCycleCallback` 중에는 `@Component` 같은 `Annotation` 이 붙어 있는 모든 `Class` 들을 찾아서
    그 클래스의 `Instance` 를 만들어서 `Bean` 으로 등록하는 `Annotation Processer` 가 등록되어 있습니다.
  * `@Repository` 는 `JPA` 가 제공해주는 기능에 의해서 `Bean` 으로 등록이 됩니다.
  * `@Configuration` 은 `Bean` 객체를 정의 할 수 있는 `Annotation` 이다.
  * `@Autowired` 는 `IoC Containner` 의 `Bean` 을 `주입` 받아서 사용할 수 있다.
  * `@Autowired` 는 `필드` 와 `Setter` 와 `생성자` 에도 사용할 수 있다.
  * `Spring` 에서 권장하는 `의존성 주입` 방법은 `생성자` 에 하는 것 이다.
  * `생성자` 를 통해 필수적으로 필요한 `Reference` 없이는 클래스를 사용할 수 없게 세팅할 수 있다
  * `생상자` 에 `의존성 주입` 시 문제가 될 수 있는 경우는 `Class` 가 서로 참조하는 `순환 참조` 가 발생할 수 있다.
    이런 경우는 둘 다 만들지 못하므로 어플리케이션이 구동이 되지 않는다.
  * `Spring` 은 크게 `Ioc`, `AOP`, `PSA` 개념들을 사용하고 있다.
    * `IoC` 는 `Inversion of Control` 의 약자이며 `의존성` 을 자기가 가지고 있는 것이 아닌 외부에 두는 것이다.
    * `AOP` 는 `Aspect Oriented Programmig` 의 약자이며 
      어떤 `로직` 을 기준으로 `핵심적인 관점`, `부가적인 관점` 으로 나누어서 보고 그 관점을 기준으로 각각 `모듈화` 하는 것이다.
      ) https://engkimbs.tistory.com/746
  * `@Transactinal` 은 `AOP` 에서 사용하는 `Annotation` 이다.
  * `StopWatch` 는 성능을 측정할 수 있는 클래스이다.
  * `AOP` 를 구현하는 방법
    * `컴파일` - `컴파일` 하는 도중에 `AOP` 작업을 한다 ( AspectJ )
    * `바이트코드 조작` - 클래스 로더가 컴파일된 클래스를 읽어올 때 `AOP` 작업을 한다
    * `프록시 패턴` - `Spirng AOP` 가 사용하는 방법으로 디자인 패턴을 사용하여 같은 효과를 낸다
  * `Spring-MVC` 의 흐름 : `Client` -> `Dispatcherservlet` -> `Handler Mapping`->
                           `Controller` -> `view` -> `Dispatcherservlet` -> `Client`
  * `@RestController` 은 `@Controller` 와  `@ResponseBody` 을 합쳐 놓은 `Annotation` 으로 
    `Spring 4.0` 버전부터 사용할 수 있다.
  * `@target` 은 해당 `Annotation` 을 어디에 쓸 것인지 정의하는 `Annotation` 이다.

 ## 다른 내용들 (추가 분류 필요)
  *  `JPA` 는 쿼리에서 스프링의 파라미터 값을 가져올때 `:파라미터` 와 같이 가져온다.
  * `Intellij` 로 `Spring MVC`, `Maven` 세팅법 https://cjh5414.github.io/intellij-spring-start/

  