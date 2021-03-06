## 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기
  ### 기존 테스트에 시큐리티 적용하기
  - @WithMockUser(roles="USER")
    - 인증된 모의(가짜) 사용자를 만들어서 사용합니다.
    - roles에 권한을 추가할 수 있습니다.
    - 즉,이 어노테이션으로 인해 ROLE_USER 권한을 가진 사용자가 API를 요청하는 것과 동일한 효과를 가지게 됩니다.
    - @WithMockUser는 MockMvc에서만 작동한다.
    - @SpringBootTest에서 MockMvc를 사용하는 방법은 따로 있다.
  - import
    - 모두 새로 추가되는 부분입니다.
    - 나머지는 기존과 동일합니다.
  - @Before
    - 매번 테스트가 시작되기 전에는 MockMvc 인스턴스를 생성합니다.
  - mvc.perform
    - 생성된 MockMvc를 통해 API를 테스트 합니다.
    - 본문(Body) 영역은 문자열로 표현하기 위해 ObjectMapper를 통해 문자열 JSON으로 변환합니다.

## AWS 서버 환경을 만들어보자 - AWS EC2
  - 클라우드 서비스란
    - 인터넷(클라우드)를 통해 서버, 스토리지(파일저장소), 데이터베이스, 네트워크, 소프트웨어, 모니터링, 등의
      컴퓨팅 서비스를 제공하는 것입니다.
    - 예를 들어 AWS의 EC2는 서버 장비를 대여하는 것이지만, 실제로는 그 안의 로그 관리.
      모니터링, 하드웨어 교체, 네트워크 관리 등을 기본적으로 지원하고 있습니다.
      개발자가 직접 해야 할 일을 AWS가 전부 지원하는 것입니다.
  - 클라우드의 형태 
    1. Infrastructure as a Service(IaaS, 아이아스, 이에스)
      - 기존 물리 장비를 미들웨어와 함께 묶어둔 추상화 서비스입니다.
      - 가상머신,스토리지,네트워크,운영체제 등의 IT 인프라를 대여해주는 서비스라고 보면 됩니다.
      - AWS의 EC2, S3 등
    2. Platform as a Service (Paas, 파스)
      - 앞에서 언급한 IaaS에서 한 번 더 추상화한 서비스입니다.
      - 한 번 더 추상화했기 때문에 __많은 기능이 자동화__ 되어 있습니다.
      - AWS의 Beanstalk(빈스톡), Heroku(헤로쿠) 등
    3. Software as a Service (SaaS 사스)
      - 소프트웨어 서비스를 이야기합니다.
      - 구글 드라이브, 드랍박스, 와탭 등
  - 이 책에서 여러 클라우드 서비스 중 AWS를 선택한 이유
    - 첫 가입 시 1년간 대부분 서비스가 무료이다. 단,서비스마다 제한이 있다.
    - 클라우드에서는 기본적으로 지원하는 기능(모니터링,로그관리,백업,복구,클러스터링 등등)이 많아 개인이나 소규모일 때
      개발에 좀 더 집중할 수 있습니다.
    - 많은 기업이 AWS로 이전 중이기 때문에 이직할 때 AWS 사용 경험은 도움이 됩니다.
      국내에서는 AWS 점유율이 압도적입니다. 쿠팡,우아한형제들,리멤버 등 클라우드를 사용할 수 있는 회사에서는
      대부분 AWS를 사용합니다.
    - 사용자가 많아 국내 자료와 커뮤니티가 활성화되어 있습니다.
  - AWS의 PaaS 서비스인 븐스톡을 사용하면 대부분 작업이 간소화되지만, 
    __프리티어로 무중단 배포가 불가능하다.__
  - 배포할 때마다 서버가 다운되면 제대로된 서비스를 만들 수 없으니 무중단 배포는 필수이고
    빈스톡은 사용할 수 없다.
  - EC2(Elastic Compute Cloud)란
    - AWS에서 제공하는 성능,용량 등을 유동적으로 사용할 수 있는 서버입니다. 보통
      "AWS에서 리눅스 서버 혹은 윈도우 서버를 사용합니다."라고 하면 이 EC2를 이야기 하는 것입니다.
      C2란 Compute Cloud에서 C가 2번 들어간다는 것을 의미한다.
  - EC2의 제한
    - 사양이 t2.micro만 가능하다.
      - vCPU(가상CPU) 1 Core, 메모리 1GB 사양입니다.
      - 보통 vCPU 는 물리 CPU 사양의 절반 정도의 성능을 가집니다.
    - 월 750시간의 제한이 있습니다. 초과하면 비용이 부과됩니다.
      - 24시간 * 31일 = 744시간입니다.
      - 즉, __1대의 t2.micro만 사용한다면 24시간__ 사용할 수 있습니다. 
  - 리전이란
    - AWS의 서비스가 구동될 지역을 이야기한다. 
      AWS는 도시별로 클라우드 센터를 지어 해당 센터에서 구축된 가상머신들을 사용할 수 있고 이걸 리전이라고 한다.
    - 서울 리전이 국내 서비스를 한다면 네트워크가 가장 빠르다.
  - 센토스 AMI가 아닌 아마존 리눅스 AMI를 사용한 이유
    - 아마존이 개발하고 있기 때문에 지원받기가 쉽다.
    - 레드햇 베이스이므로 레드햇 계열의 배포판을 많이 다뤄본 사람일수록 문제없이 사용할 수 있다.
    - AWS의 각종 서비스와의 상성이 좋다.
    - Amazon 독자적인 개발 리포지터리를 사용하고 있어 yum이 매우 빠르다.
  - 크레딧이란
    - CPU를 사용할 수 있는 포인트 개념으로 인스턴스 크기에 따라 정해진 비율로 __CPU 크레딧을 계속 받게 되며,__
      사용하지 않을 때는 크레딧을 축적하고, 사용할 때는 이 크레딧을 사용한다.
    - 정해진 사양보다 더 높은 트래픽이 오면 크레딧을 좀 더 적극적으로 사용하면서 트래픽을 처리하지만,
      __크레딧이 모두 사용되면 더이상 EC2를 사용할 수 없습니다.__
      그래서 트래픽이 높은 서비스들은 T 시리즈를 쓰지 않고 다른 시리즈를 사용하기도 한다.
    - AWS 서버는 유동 IP이므로 서버를 재시작할 때마다 IP가 바뀌게 된다.
      그럴 때는 탄련적 IP를 인스턴스에 연결함으로써 고정 IP로 사용할 수 있다.
      * 탄력적 IP는 생성하고 EC2 서버에 연결하지 않으면 비용이 발생하므로 생성할 때 무조건
        EC2에 바로 연결 해주어야 합니다.
