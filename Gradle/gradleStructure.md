## Gradle이란
  * 빌드 배포 도구이다.
  * Build Script를 통해 플러그인과 의존성 관리를 한다
  * Maven보다 좋은 점
    * 빌드 속도가 빠르다

## gradle의 구조
  * 우측에 Gradle 툴 버튼을 클릭하면 gradle의 구조를 볼 수 있다.
  * Gradle 툴에서 새로고침 버튼을 클릭하면 라이브러리를 로컬에 다운 받아 의존성 문제를 해결 가능하다.
  * `External Libraries`에는 다운 받아진 라이브러리가 자동으로 패스로 잡혀 임포트 된다.

  * gradle에서 빌드 하기
    * 패키지의 Tasks/build/ 경로에서 `build`를 더블클릭 한다.
  
  * grdle에서 프로젝트 실행하기
    * 패키지의 Tasks/application/ 폴더에 들어가 `bootRun`을 더블클릭 한다.