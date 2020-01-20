# 첫번째로 책을 폈다.

## 인텔리제이 커뮤니티 다운로드 및 실행
  - jetBrains 홈페이지에 들어가서 TOOLBOX 다운로드 후 Intellij IDEA Community를 Intall 한다.
  - TOOLBOX에서 Intellij 우측 톱니바퀴를 클릭하면 세팅을 할 수 있고
    Maximum heap size를 지정할 수 있으며 기본은 750MB이고 메모리 16기가 기준 권장량은 2048MB~4096MB이다.
  - Intellij를 처음으로 실행하면 테마를 설정할 수 있고 백기선님 유튜브에서 이쁜 걸 세팅할 수 있다.
    ( https://www.youtube.com/watch?v=sJnOdgS-wLg )
  - 단축키는 디폴드 버전으로 세팅을 한다
  - 플러그인 추가는 필요 없다.

## Gradle 세팅
  - 새로운 프로젝트를 생성을 한다
  - Gradle에서 Java를 체크 후 Next
  - ArtifactId는 원하는 이름 작성
  - 프로젝트 이름은 프로젝트 이름도 원하는 것으로 작성
  - build.gradle은 의존성을 추가하는 곳이다.
  - dependencies { }는 의존성을 넣는 곳이다.
  - ext{ }는 build.gradle에서 사용하는 전역변수를 선언하는 것이다.
  - io.spring.dependeny-management 플러그인은 스프링 부트의 의존성들을 관리해주는 플러그인이기 때문에
    반드시 추가를 해야 한다.
  - repositories는 각종 의존성 (라이브러리)들을 어떤 원격 저장소에서 받을지를 정합니다. 
  - mavenCentral은 이전부터 많이 사용했지만 본인이 만든 라이브러리를 업로드 하기 위해서는 __많은 과정과 설정이 필요__ 하다
  - jcenter는 __라이브러리 업로드를 간단하게__ 하였다. 그리고 mavenCentral에도 업로드 될 수 있게 하였기 때문에
    점점 jcenter를 많이 사용한다.
  - dependencies는 프로젝트 개발에 필요한 의존성들을 선언하는 곳이다.
  - ext를 사용하여 spring 버전을 명시한 경우 dependencies에서 굳이 버전을 지정해줄 필요가 없다.