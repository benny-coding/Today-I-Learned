## Structure
  * __DispatcherServlet__ 은 서버를 처음 실행 시에만 가장 먼저 초기화 된다
  * __DispatcherServlet__ 은 __controller__ 의 메서드를 호출한다
  * __controller__ 의 메서드는 __view__ 의 경로를 리턴한다.
  * __"redirect:/경로";__ 를 메서드의 __retrun__ 으로 사용 시 해당 페이지로 이동한다.
  * __view__ 를 나타내는 html 파일들은 __resources__ 경로에서 특정 위치에 있다.
  * __@GetMapping("경로")__ annotation은 유저가 해당 경로로 들어 왔을 때 실행될 메서드를 연결 시켜준다.
  * __application.properties__ 에 데이터베이스 이름, 스키마 경로, 데이터 경로가 정의되어 있다.
  * __db__ 는 __resource__ 패키지 밑에 위치시킨다.

## 다른 내용들 (추가 분류 필요)
  *  __JPA__ 는 쿼리에서 스프링의 파라미터 값을 가져올때 __:파라미터__ 와 같이 가져온다.
  * 