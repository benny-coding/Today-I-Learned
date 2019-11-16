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

 ## 핵심기술 
   * 스프링이란 ?
     * 소규모 어플리케이션 또는 기업용 애플리케이션을 자바로 개발하는데 있어 유용하고 편리한 기능을 제공하는 프레임워크다
   * IoC
   * AOP
   * PSA

   * IoC 컨테이너와 빈 
     * 스프링 IoC 컨테이너
       * `BeanFactory`
       * 애플리케이션 컴포넌트의 중앙 저장소
       * `Bean` 설정 소스로부터 `Bean` 정의를 읽어들이고, `Bean`을 구성하고 제공한다.
     * Bean
       * `Bean`이란 `IoC`에서 관리하고 있는 객체를 의미합니다.
       * 장점
         * 의존성 관리
         * 스코프
           * 싱글톤 : 하나만 만들어서 사용하는 것 
           * 프로포토타입 : 매번 다른 객체를 사용하는 것
         * 라이프사이클 인터페이스
       * `@Repository`와 `@Serivce`는 `@Component`를 확장한 `Annotation`이며 
         이 3가지 `Annotation`을 등록한 클래스는 `IoC`에 `Bean`으로 등록된다.
       * 위 작업들을 자바 코드 단에서 해결할 수 있도록 한 것이 
     * `@Autowired`
       * 해당 생성자, 세터, 필드에 의존성을 주입한다. 
       * 여러 개의 Bean이 있을 경우 `@Primery`를 하나의 Bean으로 의존성을 주입할 수 있다.
     * `BeanPostProccesor`
       * 빈을 만든다음에 빈에 초기화
     * `@Component`
       * basePackagesClasses에 값을 전다하면 그 클래스 기준으로 컴포넌트를 시작한다.
       * 기본 값은 @Component가 붙어 있는 클래스로부터 시작해 같은 패키지와 이하의 패키지를 모두 스캔을 시작한다.
     * @Filter
       * 
     * @ComponentScan
       * 
     * 싱글톤
       * Application 전반에 빈에 대한 인스턴스가 오직 1개 뿐이다.
     * 프로파일
      * Bean들의 묶음

      
   * 리소스
   * 데이터 바인딩
   * SpEL
   * 스프링 AOP
   * Null-Safety

 ## 다른 내용들 (추가 분류 필요)
  *  `JPA` 는 쿼리에서 스프링의 파라미터 값을 가져올때 `:파라미터` 와 같이 가져온다.
  * `Intellij` 로 `Spring MVC`, `Maven` 세팅법 https://cjh5414.github.io/intellij-spring-start/

  