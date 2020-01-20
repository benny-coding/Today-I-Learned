## Gradle 세팅
  - 의존성 입력 중에 `control + space`를 누르면 자동완성 할 수 있다
  - 우측의 Gradle 탭에서 의존성들이 잘 받아졌는지 확인이 가능하다

## Git 연동하기
  - `Command + Shift + A`를 사용하면 Action 검색창이 열린다
  - `share project on github`에서는 깃허브 원격저장소 연결과 commit, push가 가능하다
  - intellij에서는 특정 폴더나 파일을 모든 커밋 대상에서 제외할 수 있도록 하기 위해서는
    `.gitignore` 파일을 사용합니다.
  - `.ignore` plugin 설치를 위해 Action에서 plugins를 검색 후 열고 .ignore를 검색해서 설치한다.
  - 프로젝트를 우클릭 후 NEW -> .ignore.file -> .gitignore.file 을 생성하고
    만들어진 .gitignore 파일 안에서 .gradle과 같이 입력하면 .gradle은 제외가 되어 commit된다.
  - `Command + K`는 commit을 할 수 있고 `Command + Shift + K`는 push를 할 수 있다.
