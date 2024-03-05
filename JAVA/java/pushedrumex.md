<details>
  <summary>1. 가비지 컬렉션에 대해서 설명해주세요.</summary>
  Heap 영역에서 동적으로 할당했던 메모리 중 사용하지 않는 객체를 모아 주기적으로 제거하는 프로세스입니다. 이를 통해 메모리 누수를 방지할 수 있습니다. 하지만 GC 가 동작하는 동안에는 모든 애플리케이션 스레드가 중지되기 때문에 GC 가 자주 발생하면 성능에 영향을 줄 수 있습니다.
</details>
<details>
  <summary>1-1. 가비지 컬렉션 구조에 대해서 설명해주세요.</summary>
  가비지 컬렉션은 크게 young 영역과 old 영역으로 나뉩니다. young 영역은 짧게 살아남는 메모리들이 존재하는 공간으로 모든 객체는 처음에는 young 영역에 생성됩니다. old 영역은 길게 살아남는 메모리들이 존재하는 공간으로 young 영역에서 제거되지 않은 객체들이 old 영역으로 이동합니다. young 영역은 또다시 eden, survivor0, survivor1 로 나뉩니다.
</details>
<details>
  <summary>1-2. 가비지 컬렉션의 동작 과정에 대해서 설명해주세요.</summary>
  1. 모든 객체는 처음에 young 의 eden 영역에서 생성됩니다.
  2. eden 영역이 가득 차면 minor GC 가 발생합니다.
  3. 살아남은 객체들은 survivor0 영역으로 이동합니다.
  4. eden 영역이 가득 차면 minor GC 가 발생합니다.
  5. 살아남은 객체들은 survivor1 영역으로 이동합니다.
  6. 1~4 과정을 반복하다가 계속 살아남은 객체들은 old 영역으로 이동합니다.
  7. old 영역이 가득 차면 major GC 가 발생합니다.
</details>
<details>
  <summary>1-3. 가비지 컬렉션의 버전별 알고리즘을 설명해주세요.</summary>

    1. Serial GC
    - Young 영역은 Mark Sweep 알고리즘으로 수행
    - Old 영역은 Mark Sweep Compact 알고리즘으로 수행
        Compact: Heap 을 정리하기 위한 단계로, 유효한 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워서 빈공간을 확보
    - 단일 스레드로 수행되기 때문에 CPU 코어가 1개인 환경에서 사용

    2. Parallel GC
    - java 7,8 의 기본 알고리즘
      - 기본적인 처리 과정은 Serial GC 와 동일
      - Young 영역은 멀티 스레드를 통한 병렬 처리

    3. Parallel Old GC
    - Young 영역 뿐만 아니라 Old 영역도 멀티 스레드를 통한 병렬 처리
      - Old 영역에서 Mark Summary Compact 알고리즘으로 수행
        Summary: Mark 를 수행한 영역에 대해서 별도로 유효 객체를 식별

    4. CMS(Concurrent Mark Sweep) GC
    - java 9 에서 deprecated, java 14 에서 사용 중지
      - Mark Sweep 알고리즘을 Concurrent 하게 수행
      - CPU를 많이 필요로하며 Compaction 단계가 기본적으로 제공되지 않음
      - 조각난 메모리가 많을 경우 Compaction 작업을 실행하면 다른 GC보다 stop the world 시간이 증가

    5. G1(Garbage First) GC
    - java 7부터 지원, java 9 이후 기본 GC로 등극
      - Region 이라는 개념을 도입하여 Heap 영역을 균등하게 여러 Region 으로 나눔
      - garbage 가 많은(Garbage First) Region 에 대해서만 GC 를 수행하여 stop the world 시간을 줄임
      - 각 Region 을 Eden, Survivor, Available/Unused, Humongous, Old 으로 동적으로 설정

</details>

---

<details>
  <summary>2. 객체 지향 프로그래밍이란 무엇인가요?</summary>
  필요한 데이터를 추상화히켜 상태와 행위를 가진 객체를 만들고 객체들간의 상호작용을 통해 로직을 구성하는 프로그래밍 방법입니다.
</details>
<details>
  <summary>2-1. 객체 지향 프로그래밍의 특징에는 무엇이 있나요?</summary>
  1. 캡슐화: 객체의 상태와 행위를 하나로 묶어 외부에서 접근을 제어하는 것
  2. 추상화: 객체의 공통적인 특성을 추출하여 모델링하는 것
  3. 상속: 부모 클래스의 특성을 자식 클래스가 물려받는 것
  4. 다형성: 하나의 객체가 여러 가지 형태를 가질 수 있는 것
</details>
<details>
  <summary>2-2. 객체지향 프로그래밍의 장/단점에 대해서 설명해주세요.</summary>
  장점은 코드의 재사용성과 유지 보수성이 높다는 것입니다. 단점은 처리속도가 상대적으로 느리고 설계시 많은 시간이 소요된다는 것입니다.
</details>

---

<details>
  <summary>3. JVM 이 무엇인지 설명해주세요.</summary>
  운영 체제에 종속받지 않고 자바 프로그램을 실행할 수 있도록 하는 가상 머신입니다. JVM 은 메모리 관리, GC 등을 수행합니다.
</details>
<details>
  <summary>3-1. JVM 의 구성 요소에는 어떤 것들이 있나요?</summary>
    JVM 은 크게 클래스 로더, 실행 엔진, 런타임 데이터 영역으로 구성됩니다. 클래스 로더는 JVM 내로 .class 파일을 로드하고 링크를 통해 배치하며 동적으로 클래스를 로드하는 런타임 동작을 지원합니다. 실행 엔진은 클래스 로더가 로드한 바이트 코드를 실행하며 인터프리터와 JIT 컴파일러를 이용하여 기계어로 변환하고 가비지 콜렉터를 통해 더이상 사용하지 않는 인스턴스를 찾아 메모리에서 삭제합니다. 런타임 데이터 영역은 프로그램을 수행하기 위해 운영 체제에서 할당 받은 메모리 공간으로 Method Area, Heap, Stack 등으로 구성됩니다.
</details>
<details>
  <summary>3-2. java 파일이 실행되는 과정을 설명해주세요.</summary>
  1. 자바 컴파일러를 통해 .java 파일을 .class 파일로 컴파일합니다.
  2. JVM 이 .class 파일을 JIT 컴파일러로 기계어로 변환합니다.
  3. CPU 가 기계어로 변환된 코드를 실행합니다.
</details>

---

<details>
  <summary>4. 컴파일 언어란 무엇인가요?</summary>
  코드 전체를 번역하여 실행하는 언어입니다.
</details>
<details>
  <summary>4-1. 인터프리터 언어란 무엇인가요?</summary>
  코드를 한줄씩 번역하여 실행하는 언어입니다.
</details>
<details>
  <summary>4-2. 그렇다면 java 는 컴파일 언어인가요 인터프리터 언어인가요?</summary>
  java 는 컴파일 언어이자 인터프리터 언어입니다. java 는 .java 파일을 .class 파일로 컴파일하여 JVM 에서 실행되는데 이때 JIT 컴파일러를 통해 인터프리터 방식과 컴파일 방식으로 기계어로 변환됩니다.
</details>

---

<details>
  <summary>5. JVM 의 런타임 데이터 영역은 어떤 공간인가요?</summary>
  자바 프로그램을 수행하기 위해 운영 체제에서 할당 받은 메모리 공간입니다. Method Area, Heap, Stack 등으로 구성됩니다.
</details>
<details>
  <summary>5-1. Method Area 에는 어떤 것들이 저장되나요?</summary>
  클래스 정보, 메소드, 필드, 상수, static 변수 등이 저장됩니다.
</details>
<details>
  <summary>5-2. Heap 과 Stack 에는 어떤 것들이 저장되나요?</summary>
  Heap 에는 new 키워드로 생성된 객체, 배열 등이 저장됩니다. Stack 에는 지역 변수, 파라미터, 리턴 값, 연산 중 발생하는 임시 데이터 등이 저장됩니다.
</details>

---

<details>
  <summary>6. Lambda 란 무엇인가요?</summary>
  함수의 구현과 호출만으로 프로그램을 만드는 프로그램 방식으로, 함수 이름이 없이 익명함수를 만들 수 있습니다.
</details>
<details>
  <summary>6-1. 함수형 인터페이스란 무엇이고 java 에서 제공하는 함수형 인터페이스에는 어떤 것들이 있나요?</summary>
    함수형 인터페이스란 1개의 추상 메소드를 갖는 인터페이스를 말합니다. FunctionalInterface 애노테이션을 사용하여 함수형 인터페이스임을 명시할 수 있습니다. java 가 기본적으로 제공하는 함수형 인터페이스에는 Comparator, Predicate, Runnable 등이 있습니다.

    1. Comparator: T 타입 인자를 두 개 받아서 int 타입을 반환 (T, T) -> int
    2. Predicate: T 타입 인자를 받아서 boolean 타입을 반환 T -> boolean
    3. Runnable: 인자를 받지 않고 void 를 반환하는 메소드를 가진 인터페이스
</details>

---

<details>
  <summary>7. 자바에서 가시성 문제와 동시성 문제가 무엇이며 언제 발생하는지 설명해주세요.</summary>
  가시성 문제는 멀티 코어 시스템에서 발생하는 문제입니다. 각각의 코어는 자신만의 캐시 메모리를 가지고 있으며 여러 스레드의 캐시 메모리에 있는 값이 달라 가시성 문제가 발생할 수 있습니다.<br>
  동시성 문제는 여러 스레드에서 공유자원을 동시에 접근하였을 때 연산이 가장 늦게 끝난 스레드의 결과가 덮어씌워지는 문제입니다.
</details>
<details>
  <summary>7-1. 자바에서 가시성 문제와 동시성 문제를 해결할 수 있는 방법을 알고 계신가요?</summary>
  synchronized, volatile, Atomic Type 이 있습니다.<br>
  synchronized 는 메서드나 블록을 한 번에 한 스레드만 수행하도록 보장합니다. 단점은 대기중인 스레드가 많아질수록 성능이 저하됩니다.<br>
  volatile 은 변수 앞에 volatile 키워드를 붙여 선언하여 변수의 값을 읽거나 쓸 때 CPU 캐시가 아닌 메인 메모리에서 직접 읽거나 쓰도록 합니다. 가시성 문제는 해결되지만 동시성 문제는 해결되지 않습니다.<br>
  Atomic Type 은 java.util.concurrent.atomic 패키지에 있는 클래스들로 CAS(Compare And Swap) 알고리즘을 통해 가시성 문제와 동시성 문제를 해결할 수 있습니다.
</details>
<details>
  <summary>7-1. CAS 알고리즘에 대해 설명해주세요.</summary>
  현재 스레드가 존재하는 CPU 의 캐시 메모리와 메인 메모리에 저장된 값을 비교하여 같으면 새로운 값으로 교체하고 일치하지 않을 경우 새로 바뀐 값을 읽어와서 다시 시도하는 알고리즘입니다.
</details>

