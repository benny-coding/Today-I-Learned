## Structure
  * __DispatcherServlet__ 은 서버를 처음 실행 시에만 가장 먼저 초기화 된다
  * __DispatcherServlet__ 은 __controller__ 의 메서드를 호출한다
  * __controller__ 의 메서드는 __view__ 의 경로를 리턴한다.
  * __"redirect:/경로";__ 를 메서드의 __retrun__ 으로 사용 시 해당 페이지로 이동한다.
  * __view__ 를 나타내는 HTML 파일들은 __resources__ 경로에서 특정 위치에 있다.
  * __@GetMapping("경로")__ __Annotation__ 은 유저가 해당 경로로 들어 왔을 때 실행될 메서드를 연결 시켜준다.
  * __application.properties__ 에 데이터베이스 이름, 스키마 경로, 데이터 경로가 정의되어 있다.
  * __db__ 는 __resource__ 패키지 밑에 위치시킨다.
  * __IoC__ 는 __의존성__ 을 자기가 가지고 있는 것이 아닌 외부에 두는 것이다.
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
 ## 다른 내용들 (추가 분류 필요)
  *  __JPA__ 는 쿼리에서 스프링의 파라미터 값을 가져올때 __:파라미터__ 와 같이 가져온다.
  * 