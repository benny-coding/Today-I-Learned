## Structure
  * __DispatcherServlet__ 은 서버를 처음 실행 시에만 가장 먼저 초기화 된다
  * __DispatcherServlet__ 은 __controller__ 의 메서드를 호출한다
  * __controller__ 의 메서드는 __view__ 의 경로를 리턴한다.
  * __"redirect:/경로";__ 를 메서드의 __retrun__ 으로 사용 시 해당 페이지로 이동한다.
  * __view__ 를 나타내는 HTML 파일들은 __resources__ 경로에서 특정 위치에 있다.
  * __@GetMapping("경로")__ __Annotation__ 은 유저가 해당 경로로 들어 왔을 때 실행될 메서드를 연결 시켜준다.
  * __application.properties__ 에 데이터베이스 이름, 스키마 경로, 데이터 경로가 정의되어 있다.
  * __db__ 는 __resource__ 패키지 밑에 위치시킨다.
  * __Bean__ 은 __Spring__ 가 관리하는 __객체__ 를 의미한다.
  * __IoC Container__ 는 __BeanFactory__ 이고 __ApplicationContext__ 는 __BeanFactory__ 를 상속 받고 있다.
  * __IoC Container__ 의 일은 __Bean__ 을 만들고 __의존성__ 을 엮어주며 그 __Bean__ 들을 제공해준다.
  * __Bean__ 으로 등록된 클래스들은 __Intellij__ 에서 좌측에 줄번호 옆에 초록색으로 표시 되어 있다.
  * __의존성 주입__ 은 __Bean__ 끼리만 가능하다. 즉 __IoC Container__ 안에 있는 객체 끼리만 의존성이 가능하다.
  * __Spring__ 에서의 __Bean__ 은 __ApplicationContext__ 가 알고 있는 객체이다.
  * __Bean__ 을 등록하는 방법은 2가지가 있다.
    * __Component Scanning( @Component )__ 
      * __@Repository__
      * __@Servicee__
      * __@Controller__
    * 직접 일일히 __XML__ 이나 자바 설정 파일에 __Bean__ 으로 등록
  * __Annotation processer__ 중 __Spring IoC Container__ 가 사용하는 여러가지 __Interface__ 가 있다.
    그런 __Interface__ 들을 우리는 __LifeCycleCallback__ 이라 한다
  * 여러가지 __LifeCycleCallback__ 중에는 __@Component__ 같은 __Annotation__ 이 붙어 있는 모든 __Class__ 들을 찾아서
    그 클래스의 __Instance__ 를 만들어서 __Bean__ 으로 등록하는 __Annotation Processer__ 가 등록되어 있습니다.
  * __@Repository__ 는 __JPA__ 가 제공해주는 기능에 의해서 __Bean__ 으로 등록이 됩니다.
  * __@Configuration__ 은 __Bean__ 객체를 정의 할 수 있는 __Annotation__ 이다.
  * __@Autowired__ 는 __IoC Containner__ 의 __Bean__ 을 __주입__ 받아서 사용할 수 있다.
  * __@Autowired__ 는 __필드__ 와 __Setter__ 와 __생성자__ 에도 사용할 수 있다.
  * __Spring__ 에서 권장하는 __의존성 주입__ 방법은 __생성자__ 에 하는 것 이다.
  * __생성자__ 를 통해 필수적으로 필요한 __Reference__ 없이는 클래스를 사용할 수 없게 세팅할 수 있다
  * __생상자__ 에 __의존성 주입__ 시 문제가 될 수 있는 경우는 __Class__ 가 서로 참조하는 __순환 참조__ 가 발생할 수 있다.
    이런 경우는 둘 다 만들지 못하므로 어플리케이션이 구동이 되지 않는다.
  * __Spring__ 은 크게 __Ioc__, __AOP__, __PSA__ 개념들을 사용하고 있다.
    * __IoC__ 는 __Inversion of Control__ 의 약자이며 __의존성__ 을 자기가 가지고 있는 것이 아닌 외부에 두는 것이다.
    * __AOP__ 는 __Aspect Oriented Programmig__ 의 약자이며 
      어떤 __로직__ 을 기준으로 __핵심적인 관점__, __부가적인 관점__ 으로 나누어서 보고 그 관점을 기준으로 각각 __모듈화__ 하는 것이다.
      ) https://engkimbs.tistory.com/746
  * __@Transactinal__ 은 __AOP__ 에서 사용하는 __Annotation__ 이다.
  * __StopWatch__ 는 성능을 측정할 수 있는 클래스이다.
  * __AOP__ 를 구현하는 방법
    * __컴파일__ - __컴파일__ 하는 도중에 __AOP__ 작업을 한다 ( AspectJ )
    * __바이트코드 조작__ - 클래스 로더가 컴파일된 클래스를 읽어올 때 __AOP__ 작업을 한다
    * __프록시 패턴__ - __Spirng AOP__ 가 사용하는 방법으로 디자인 패턴을 사용하여 같은 효과를 낸다
  * __Spring-MVC__ 의 흐름 : __Client__ -> __Dispatcherservlet__ -> __Handler Mapping__->
                           __Controller__ -> __view__ -> __Dispatcherservlet__ -> __Client__
  * __@RestController__ 은 __@Controller__ 와  __@ResponseBody__ 을 합쳐 놓은 __Annotation__ 으로 
    __Spring 4.0__ 버전부터 사용할 수 있다.
  * __@target__ 은 해당 __Annotation__ 을 어디에 쓸 것인지 정의하는 __Annotation__ 이다.

 ## 다른 내용들 (추가 분류 필요)
  *  __JPA__ 는 쿼리에서 스프링의 파라미터 값을 가져올때 __:파라미터__ 와 같이 가져온다.
  * __Intellij__ 로 __Spring MVC__, __Maven__ 세팅법 https://cjh5414.github.io/intellij-spring-start/

  