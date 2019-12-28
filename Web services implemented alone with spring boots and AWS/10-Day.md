## 머스테치로 화면 구성하기
  ### 게시글 등록 화면 만들기
  - js 파일에서 function을 추가할 때 변수의 속성으로 추가를 한다.
    다른 js 파일에서 같은 init과 function이 있을 때 마지막에 실행된 파일에
    덮어씌워지기 때문이다. 

    여러 사람이 참여하는 프로젝트에서 중복된 함수명은 자주 발생할 수 있는 문제이고
    모든 함수명을 확인하면서 만들 수는 없습니다. js 파읾만의 유효범위(scope)를 만들어 사용한다.

    방법은 `var index` 객체를 만들어 해당 객체에 필요한 모든 function을 선언하는 것이다.
    이렇게 하면 index 객체 안에서만 function이 유효하다.

  - `index.js` 호출 코드를 보면 __절대 경로(/)__ 로 바로 시작한다.
    스프링 부트는 기본적으로 src/main/resources/static에 위치한 자바스크립트, CSS, 이미지 등
    정적 파일들은 URL에서 /로 설정됩니다.
  - js, css, image 경로
    - `src/main/resources/static/js/`은 `(http://도메인/js/)` 경로와 같다.
    - `src/main/resources/static/css/`은 `(http://도메인/css/)` 경로와 같다.
    - `src/main/resources/static/image/`은 `(http://도메인/image/)` 경로와 같다.
  - __{{#posts}}__
    - posts라는 List를 순회합니다.
    - Java의 for문과 동일하게 생각하면 됩니다.
  - __{{id}} 등의 {{변수명}}__
    - List에서 뽑아낸 객체의 필드를 사용합니다.
  - SpringDataJpa에서 제공하지 않는 메소드는 @Query를 사용할 수 있다.
  - `@Transactional`에 옵션을 readOnly = true로 주면 트랜잭션 범위는 유지하되
    조회 기능만 남겨두어 조회 속도가 개선되기 때문에 CRUD 중 Read만 있는 서비스 메소드에 사용을 추천한다.
  - `.map(PostsListRespnseDto::new)` -> `.map(posts -> new PostsListResponseDto(posts))`

    
