## 머스테치로 화면 구성하기
  ### 게시글 조회 화면 만들기
  - __Model__
    - 서버 템플릿 엔진에서 사용할 수 있는 객체를 저장할 수 있습니다.
    - 여기서는 postsService.findAllDesc()로 가져온 결과를 posts로 index.mustache에 전달합니다.