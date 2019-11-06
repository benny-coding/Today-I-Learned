## Structure
  * __DispatcherServlet__ 은 서버를 처음 실행 시에만 가장 먼저 초기화 된다
  * __DispatcherServlet__ 은 __controller__ 의 메서드를 호출한다
  * __controller__ 의 메서드는 __view__ 의 경로를 리턴한다.
  * __view__ 를 나타내는 html 파일들은 __resources__ 경로에서 특정 위치에 있다.
