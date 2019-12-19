## 박싱된 기본 타입보다는 기본 타입을 사용하라
  ### 서론
  - 자바의 데이터 타입은 크게 __기본 타입(Primitive type)__ 과 __참조 타입(Reference Type)__ 으로 구분된다.
  #### 기본 타입(Primitive type)
    - int
    - long
    - short
    - double
    - char
    - boolean

  #### 참조 타입(Reference Type)
    - String
    - Integer
    - Long
    - Double
    - Boolean

  ### 기본 타입 VS 참조타입
    - 기본 타입은 값만 가지고 있으나, 박싱된 기본 타입은 값에 더해 식별성(identity)란 속성을 갖는다.
      - 기본 타입은 흔히 말하는 리터럴(Literal)이다.
        > 리터럴이란 
        > 소스 코드의 고정된 값을 의미하는 용어이다(상수 또는 변수에 할당할 수 있는 값 자체를 일컫는 용어)
      - 기본 타입의 값은 JVM내의 Stack 메모리에 저장된다.
      - 참조 타입의 값은 객체 내의 상수에 저장된다. 따라서 JVM 내의 Heap 메모리에 저장된다.
      - 따라서 박싱된 타입의 객체는 같은 값이라 하더라도 다른 개겣일 경우에는 다르다고 식별이 가능하다.
    - 기본 타입의 값은 언제나 유효한 값을 가지고 있으나 박싱된 기본타입은 유효하지 않을 수 있다.
      - 기본타입의 값은 Java의 경우 초기화 되지 않으면 0으로 초기화 된다.
      - 박싱된 기본 타입의 경우에는 초기화 되지 않으면 null이 될 수 있다.
    - 기본 타입이 박싱된 기본 타입보다 시간과 메모리 사용면에서 더 효율적이다.
      - 박싱된 타입은 heap에 객체를 생성하기 때문에 메모리 사용면에서 더 안좋다.
      - 기본타입은 변수에 값이 있는 반면, 박싱된 기본 타입은 변수의 객체참조 정보를 바탕으로 heap에서 찾으므로
        시간적인 측면에서 기본타입보다 값에 접근하는 시간이 더 들게 된다.

  ### 잘못 구현된 비교자 예제
  ```java
    Comparator<Integer> naturalOrder = (i,j) -> (i < j) ?  -1 : (i == j ? 0 : 1);
  ```
    - 위의 코드를 기반으로 Integer 비교가 실행되면 같은 값을 비교한다고 해도 1이 나올 수 있다.
    - 첫번째 i < j 에 대한 연산 시, Integer타입인 i와 j는 기본타입 int로 언박싱된다.
    - 첫번째 연산이 false이면 두번째 연산 i == j 에서도 false가 발생하게 된다.
    - 이유는, (i, j)의 타입이 Integer로 추론되기 때문에 i == j 연산이 이루어질 때 객체의 동일성검사가 이루어져
      false가 발생하기 때문이다. (i와 j는 내부 값은 같지만 서로 다른 객체이기 때문이다.)

  __이처럼 같은 객체가 아니라면 박싱된 기본타입에 ==연산자를 이용하여 비교하면 예상과는 다른 결과가 나올 수 있다.__

  ```java
    Comparator<Integer> naturalOrder = (i, j) -> {
        int unBoxi = i;
        int unBoxj = j;
        return (unBoxi < unBoxj) ? -1 : (unBoxi == unBoxj ? 0 : 1);
    }
  ```
  위와 같이 수정하면 정상적인 결과를 얻을 수 있다.

  ## 갑자기 발생하는 NullPointerException
  ```java
    public class Unbelievable {
        static Integer i;

        public static void main(String[] args){
            if(i == 42){
                System.out.println("믿을 수 없군");
            }
        }
    }
  ```
  이 프로그램은 "믿을 수 없군"을 출력하지는 않지만, 전혀 예상하지 못한 결과를 보여준다.
  i == 42를 검사하는 과정에서 NullPointerException을 던진다.
  원인은 i가 literal 값인 42와 비교하는 과정에서 i는 Auto UnBoxing을 수행한다.
  하지만 i는 null이기 때문에 Auto UnBoxing을 수행하는 과정에서 NullPointerException을 발생시키게 된다.

  __기본 타입과 박싱된 기본 타입을 혼용한 연산에서는 박싱된 기본 타입의 박싱이 자동으로 풀린다.__
  하지만 박싱된 기본 타입이 null인 경우에는 NullPointerException이 발생하니 주의 해야 한다.

  ## 의도하지 않은 Auto Boxing으로 인한 성능저하
  ```java
    public static void main(String[] args){
        Long sum = 0L;
        for (Long i = 0L; i < Integer.MAX_VALUE; i++){
            sum += i;
        }
        System.out.println(sum);
    }
  ```
  위 코드는 sum을 Long으로 선언하였기 때문에 엄청난 성능상 안좋은 코드이다.
  sum += i;를 수행하는 과정에서 __sum이 long타입으로 UnBoxing되고__ sum + i 연산이 이루어진다음
  __Long타입으로 AutoBoxing되기 때문이다.__

  ## 박싱된 기본타입은 언제 사용해야 하는가?
    - 컬렉션 원소, 키, 값으로 쓴다.
      - 컬렉션은 기본타입을 담을 수 없으므로 어쩔 수 없이 박싱된 기본타입을 사용해야 한다.
    - 제네릭(Generics) 타입을 이용하는 경우에도 박싱된 기본타입을 사용한다.
      - 제니릭 타입에서는 int, double과 같은 기본타입을 지원하지 않기 때문이다.
    - 리플렉션(Reflection)을 통해 메서드를 호출할 때에도 박싱된 기본타입을 사용한다.

  ## 정리
    - 기본 타입과 박싱된 기본 타입을 사용해야 한다면, 가능하면 기본 타입을 사용하는 것이 좋다.
    - 기본타입은 간단하고 빠르다.
    - 박싱된 기본 타입을 사용한다면 주의를 기울이자
    - AutoBoxing이 기본타입을 변경할 때 번거로움을 줄여주지만 그 위험까지 없애주지는 않는다.
      - 박싱된 기본 타입을 == 연산자로 비교한다면 객체의 동일성 비교가 이뤄지는데
        개발자가 의도한 결과가 나오지 않을 가능성이 크다.
      - == 연산에서 기본 타입과 박싱된 기본 타입의 연산이 이루어지면, 박싱된 기본 타입이 UnBoxing되는데
        박싱된 기본 타입이 null인 경우 NullPointerException이 발생한다.
    - 기본 타입을 Boxing하느 것은 필요없는 객체를 생성하는 부작용이 나올 수 있다.


  ## References
    - __[Carrey's 기술블로그] https://jaehun2841.github.io/2019/03/01/effective-jave-item61/#%EA%B8%B0%EB%B3%B8-%ED%83%80%EC%9E%85-primitive-type__
