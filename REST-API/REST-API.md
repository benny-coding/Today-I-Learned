# REST API

## REST API의 구성
  * __자원(RESOURCE) - URI__
  * __행위(Verb) - HTTP METHOD__
  * __표현(Representations)__

## REST의 특징
  * Uniform(유니폼 인터페이스)
    * `URI` 로 지정한 리소스 에 대한 조작을 __통일되고 한정적인 인터페이스 로 수행하는__ `아키텍처 스타일` 을 말합니다.
  * stateless(무상태성)
    * `REST` 는 `무상태성` 성격을 갖습니다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다.
      `세션 정보` 나 `쿠키 정보` 를 별도로 저장하고 관리하지 않기 때문에 __API 서버는 들어오는 요청만을 단순히 처리__ 하면 됩니다.
      때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해집니다.
  * Cacheable(캐시 가능)
    * REST의 가장 큰 특징 중 하나는 `HTTP` 라는 기존 웹 표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로
      활용이 가능합니다. 따라서 HTTP가 가진 `캐싱 기능` 이 적용 가능합니다. HTTP 프로토콜 표준에서는 사용하는 Last-Modified태그나
      E-Tag를 이용하면 캐싱 구현이 가능합니다.
  * Self-descriptiveness(자체 표현 구조)
    * REST의 또 다른 큰 특징 중 하나는 __REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는__
      `자체 표현 구조` 로 되어 있다는 것입니다.
  * Client - Server 구조
    * REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로
      각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용을 명확해지고 서로간 의존성이 줄어들게 됩니다.
  * 계층형 구조
    * REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고
      PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

## REST API 디자인 가이드
  * URI는 정보의 __자원을 표현 해야 한다.__
  * 자원에 대한 행위는 `HTTP Method(GET,POST,PUT,DELETE)` 로 표현해야 한다.
    * POST - URI를 요청하면 리소스를 `생성` 
    * GET - 리소스를 `조회`
    * PUT - 리소스를 `수정`
    * DELETE - 리소스를 `삭제`
  * 예제
    * 회원정보를 가져오는 URI - `GET /meembers/1`
    * 회원을 추가하는 URI - `POST /members/2`
  * URI 설계 시 주의할 점
    * 구분자 `/` 는 계층 관계를 나타내는데 사용
    * URI 마지막 문자로 `/` 를 포함하지 않는다.
    * `-` 은 `URI 가독성` 을 높이는데 사용
    * `( _ )` 밑줄은 URI에 사용하지 않는다.
    * URI 경로에는 소문자가 적합하다.
    * 파일 확장자는 URI에 포함시키지 않는다.
  * 리소스 간의 관계를 표현하는 방법
    * `GET : /users/{userid}/devices` (일반적인 소유 'has'의 관계를 표현할 때)
      - 해석 : users 중 하나인 {userid}의 devices 
    * `GET : /users/{userid}/likes/devices` (관계명이 애매하거나 구체적 표현이 필요할 때)
      - 해석 : users 중 하나인 {userid}가 likes하는 diesces
  * 자원을 표현하는 `Collection` 과 `Document`
    * `http://restapi.example.com/sports/soccer/players/13` 에서 
      sports와 players는 `Collection` soccer과 13은 `Document` 이다 
      ( `Collection` 은 복수형으로 사용한다 )
  * HTTP 응답 상태 코드
    * `200` : 클라이언트의 요청을 정상적으로 수행
    * `201` : 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨
                (POST를 통한 리소스 생성 작업 시)
    * `400` : 클라이언트의 요청이 부적절 할 경우
    * `401` : 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때
                (로그인 하지 않은 유저가 로그인 했을 때, 요청가능한 리소스를 요청했을 때)
    * `403` : 유저 인증상태와 관계 없이 응답하고 싶지 않은 리소스를 클라이언트가 요청했을 때
                (403 보다는 400이나 404를 사용할 것을 권고, 403 자체가 리소스가 존재한다는 뜻이기 때문에)
    * `405` : 클라이언트가 요청한 리소스에서는  사용 불가능한 Method를 이용했을 경우 사용하는 응답코드 
    * `301` : 클라이언트가 요청한 리소스에 대한 URI가 변경 되었을 때 사용하는 응답 코드
                (응답 시 Location header에 변경된 URI를 적어 줘야 합니다.)
    * `500` : 서버에 문제가 있을 경우 사용하는 응답 코드

## 그런 REST API로 괜찮은가
  * API란?
    * `Application Programming Interface`의 약자로

  * REST란?
    * `REpresentational State Transfer`의 약자이며 직역하자면 `대표적인 상태 이전`이다.
    * 인터넷 상의 시스템 간의 상호 윤용성(interoperabillty)을 제공하는 방법중 하나
    * 시스템 제각각의 독립적인 진화를 보장하기 위한 방법
    * REST API : REST 아키텍쳐 스타일을 따르는 API이다

  * REST 아키텍처 스타일 
    * Client-Server
    * Stateless
    * Cache
    * Uniform Interface
    * Layered System
    * Code-On-Demand (optional)

  * Uniform Interface
    * Identification of resources
    * manipulation of resources through represenations
    * __self-descritive messages__
    * __hypermisa as the engine of application state (HATEOAS)__

  * 위 두가지 제약에 대해서 제대로 이루어지지 않고 있다.
    * Self-descriptive message
      * 메시지 스스로 메시지에 대한 설명이 가능해야 한다.
      * 서버가 변해서 메시지가 변해도 클라이언트는 그 메시지를 보고 해석이 가능하다.
      * 확장 가능한 커뮤니케이션
    * HATEOAS
      * 하이퍼미디어(링크)를 통해 애플리케이션 상태 변화가 가능해야 한다.
      * 링크 정보를 동적으로 바꿀 수 있다. (Versioning 할 필요 없이)

  * Self-descriptive message 해결 방법
    1. 미디어 타입을 정의하고 IANA에 등록하고 그 미디어 타입을 리소스 리턴 시
       Content-Type으로 사용한다.
    2. profile 링크 헤더를 추가한다.
      * 브라우저들이 아직 스팩 지원을 잘 안해
      * 대안으로 HAL의 링크 데이터에 profile 링크 추가

  * HATEOAS 해결 방법
    * 방법1 : 데이터에 링크 제공
      * 링크를 어떻게 정의할 것인가? HAL


## 본 받을만한 깃허브의 REST API 
  * developer.github.com/v3/issues/

## 출처 
  * https://meetup.toast.com/posts/92
  * https://www.youtube.com/watch?v=RP_f5dMoHFc 

   