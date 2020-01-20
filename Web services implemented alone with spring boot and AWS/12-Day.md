## 머스테치로 화면 구성하기
  ### 게시글 조회 화면 만들기
  - __{{post.id}}__
    - 머스테치는 객체의 필드 접근 시 점(Dot)으로 구분합니다.
    - 즉, Post 클래스의 id에 대한 접근은 post.id로 사용할 수 있습니다.
  - __readonly__
    - Input 태그에 읽기 가능만 허용하는 속성

  - __$('#btn-update').on('click')__
    - btn-update란 id를 가진 HTML 엘리먼트에 click 이벤트가 발생할 때 
      update function을 실행하도록 이벤트를 등록합니다.
  - __update: function ()__
    - 신규로 추가될 update function입니다.
  - __type:'PUT'__
    - 여러 HTTP Method 중 PUT 메소드를 선택합니다.
    - PostsApiController에 있는 API에서 이미 @PutMapping으로 선언했기 때문에
      PUT을 사용해야 합니다. 참고로 이는 REST 규약에 맞게 설정된 것입니다.
    - REST에서 CRUD는 다음과 같이 HTTP Method에 매핑됩니다.
      생성 (create) - POST
      읽기 (Read) - GET
      수정 (Update) - PUT
      삭제 (Delete) - DELETE
  - url: '/api/v1/posts/' + id
    - 어느 게시글을 수정할지 URL Path로 구분하기 위해 Path에 id를 추가합니다.
