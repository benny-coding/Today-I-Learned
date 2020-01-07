## 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기
  ### 구글 로그인 연동하기
  - __(User) httpSession.getAttribute("user")__
    - 앞서 작성된 CustomOAuth2UserService에서 로그인 성공 시 세션에
      SessionUser를 저장하도록 구성했습니다.
    - 즉, 로그인 성공 시 httpSession.getAttribute("user")에서 값을 가져올 수 있습니다.
  - __if (user != null)__
    - 세션에 저장된 값이 있을 때만 model에 userName으로 등록합니다.
    - 세션에 저장된 값이 없으면 model엔 아무런 값이 없는 상태이니 로그인 버튼이 보이게 됩니다.