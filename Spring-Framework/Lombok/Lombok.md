# Lombok

  * Lombok이란?
    * `Lombok` 은 자바에서 `@Getter`, `@Setter` 같은 `annotation` 기반으로 기존 `DTO`, `VO`, `Domain Class` 작성 할 때,
      멤버변수에 대한 Getter/Setter Method, Equeals(), hashCode(), ToString()과 멤버 변수에 값을 설정하는 생성자 등등을
      자동으로 생성해주는 라이브러리
  * 기능 (annotation)
    * @Getter @Setter : `Getter`, `Setter` 메소드 자동 생성
    * @ToString : `ToString` 메소드 자동생성
    * @EqualsAndHashCode : `equals, hashcode 메소드 자동생성
    * @Data : `@ToString`, `@EquealsAnsHashCode`, `@Getter`,
              `@Setter`, `@RequiredArgsConstructor` 자동 생성
    * @val : `final` 키워드 대신 사용하는 변수 선언 `class`
    * @NonNull : 해당 값이 `Null` 일경우 `NullPointerException`을 발생
    * @Cleanup : 자동 리소스 관리 : `close()` 메소드를 귀찮음 없게 안전하게 호출
    * @EqualsAndHashCode : `Hashcode` 와 `equals` 메소드를 생성
    * @NoArgsContructor : 인자 없는 생성자 생성
    * @RequriedArgsConstructor : 필수 인자만 있는 생성자 생성(다른 생성자가 없을 때에만 만들어짐)
    * @AllArgsConstructor : 모든 인자를 가진 생성자 생성
    * @Value : 불편 클래스를 쉽게 생성
    * @Builder : Builder API처럼 사용할 수 있도록 지원
    * @SneakyThrows : Exception 발생시 체크된 Throable로 감싸서 전달
    * @Synchroniczed : 메소드에서 동기화 Lock을 설정
    * @Log : 종류별 로그를 사용할 수 있도록 한다.
* ex) CODE

    ```java
    @Data
    @ToString(exclude = {"name", "address"}, includeFieldNames = false, callSuper = true)
    @EqualsAndHashCode(of = {"name", "address"}, exclude = {"gender", "phone"})
    public class LombokGsonSampleInfo {

        private String id;
        @Getter(AccessLevel.PRIVATE) @Setter(AccessLevel.PUBLIC)
        private String name;

        @NonNull
        private String email;   // 메소드의 인자가 null일 경우 Exception을 출력한다.
                                // (java.lang.NullPointerException)
        private String address;
        private Stirng gender;
        private Phone phone
    }
    ```
* IntelliJ 설치 방법
    * `Maven` 에서는 `pom.xml` 에 `dependency(의존성)` 을 추가해야 한다.
    ```xml
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.16.16</version>
        <scope>provided</scope>
    </deependency>
    ```
    * 1. `plugin`에서 `Lombok` 플러그인을 설치한다.
    * 2. `Preference` -> `Build, Excution, Deployment` -> `Compiler` -> `Annotation Processors`
         -> `Enable annotation processing` 체크 후 OK 하고 정상 작동 확인

## 출처 - https://meetup.toast.com/posts/92