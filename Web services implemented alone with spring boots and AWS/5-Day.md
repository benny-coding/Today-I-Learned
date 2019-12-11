## Hello Controller 코드 롬복으로 전환
  - Junit과 비교하여 assertj의 장점
    - CoreMatchers와 달리 추가적으로 라이브러리가 필요하지 않습니다.
      - Junit의 assertThat을 쓰게 되면 is()와 같이 CoreMatchers 라이브러리가 필요합니다.
    - 자동완성이 좀 더 확실하게 지원됩니다.
      - IDE에서는 CoreMatchers와 같은 Matcher 라이브러리의 자동완성 지원이 약합니다.
    - assertj의 장점에 대한 자세한 설명은 백기선님의 유튜브 
      'ssertJ가 JUnit의 assertThat 보다 편리한 이유'를 참고하시면 좋습니다.