## try-with-resources
  * 운영체제는 자원을 할당 받아 동작한다.
  * 자원을 사용한 후 반납하지 않은 자원들을 계속해서 쌓이게 되며
    결국 모든 자원을 사용하여 문제를 발생시킨다.
  * 이 중의 가장 많은 문제를 발생시키는 것이 입출력 자원이다.
    * 스트림이라는 데이터를 주고 받는 통로를 열어야 하는데 그 통로가 입출력 자원이다.
    * 이러한 입출력들은 자원을 많이 소모 하므로 완료되면 꼭 해당 자원을 돌려주어야 한다.
  * 입출력 수행하는 중에 에러가 난다면 어떻게 예외처리하는가?
    * 특별한 처리를 해주지 않는다면 스트림이 open 상태로 남겨지게 된다.
  
  * 일반적인 예외처리 (소스가 엄청 복잡하다)
  
  ```java
    FileoutputStream out = null;
    try {
        out = new FileoutputStream("exFile.txt");
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } finally {

        if(out != null) {
            try {
                out.close(); // close 하다가 예외 발생 가능성 있음
            } catch(IOException e){
                e.printStackTrace();
            }
        }
    }
  ```

  * try - with - resources 구문 적용 시
  ```java
    try(FileOutputStream out = new FileOutputStream("exFile.txt")) {
        // 로직 처리
    } catch(IOException e){
        e.printStackTrace();
    }
  ```

  * 우선 코드가 많이 줄었고 try문이 끝나면 자동으로 close()를 해준다.
    try 구문에 `AutoCloseable` 인터페이스가 JDK 1.7부터 추가 되었기에
    가능하다

## 출처1 - https://dololak.tistory.com/67
## 출처2 - https://ryan-han.com/post/java/try_with_resources/