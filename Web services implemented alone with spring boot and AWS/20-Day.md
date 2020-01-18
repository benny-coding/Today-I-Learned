## 스프링 시큐리티와 OAuth 2.0으로 로그인 기능 구현하기
  ### 네이버 로그인
  - 네이버 오픈 API로 이동해서 등록하기
    - `https://developers.naver.com/apps/#/register?api=nvlogin` 접속하여 
      로그인 후 각 항목들을 입력한다. 
    - user_name_attribute=response
      - 기준이 되는 user_name의 이름을 네이버에서는 response로 해야 합니다.
      - 이유는 네이버 회원 조회 시 반환되는 JSON 형태 때문입니다.
      - 스프링 시큐리티에선 하위 필드를 명시할 수 없다. 하지만 네이버의 응답값 최상위 클래스 필드는 
        resultCode, message, response 이 세가지이므로 user_name을 response로 한다.
        그 후 자바 코드로 response의 id를 user_name으로 지정한다.
      - /oauth2/authorization/naver