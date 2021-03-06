## JVM이란
  * JVM이란 JAVA Virtual Machine, 자바 가상 머신의 약자를 따서 줄여 부르는 용어이다 
    (가상머신이란 프로그램을 실행하기 위해 물리적 머신과 유사한 머신을 소프트웨어로 구현한 것이다.)
    JVM 역할은 자바 애플리케이션은 클래스 로더를 통해 읽어 들여 자바 API와 함께 실행하는 것이다.
    그리고 JVM은 JAVA와 OS 사이에서 중개자 역할을 하며 JAVA가 OS에 구애받지 않고 재사용을 가능하게 해준다
    그리고 가장 중요한 메모리관리, Garbage collection을 수행한다. 그리고 JVM은 스택기반 가상머신이다.
    ARM 아키텍쳐 같은 하드웨어는 레지스터 기반으로 동작하는데 비해 JVM은 스택기반으로 동작한다.

  * 왜 자바 가상머신을 알아야 하는가?
    * 한정된 메모리를 효율적으로 사용하여 최고의 성능을 내기 위해서가 그 답이 될지 모르겠다.
      메모리 효율성을 위해 메모리 구조를 알아야 하기 때문이다. 동일한 기능의 프로그램이더라도 메모리 관리에 따라
      성능이 좌우된다. 메모리 관리가 되지 않은 경우 속도저하 현상이나 튕김 현상 등이 일어날 수 있다. 그래서,
      알아두면 좋다를 넘어서 알아야 하는 것이다.

  * 자바프로그램 실행과정
    1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다.
       JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
    2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환시킨다.
    3. Class Loader를 통해 class 파일들을 JVM으로 로딩한다.
    4. 로딩된 class 파일들은 Excution engine을 통해 해석된다.
    5. 해석된 바이트코드는 Runtime Data Areas 에 배치되어 실질적인 수행이 이루어지게 된다.
       이러한 실행과정 속에서 JVM은 필요에 따라 Tread Synchronization과 GC같은 관리 작업을 수행한다.