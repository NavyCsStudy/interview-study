<details>
  <summary>1. JVM의 구조</summary>
  <li> Class Loader:<ul>
    <li> JVM 내로 클래스 파일을 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈</li>
    <li> 런타임 시에 동적으로 클래스를 로드한다.</li></ul></li>
<li> Execution Engine:<ul>
    <li> 클래스 로더를 통해 JVM 내의 Runtime Data Area에 배치된 바이트 코드들을 명렁어 단위로 읽어서 실행</li>
    <li> 인터프리터 방식, JIT 컴파일러 방식</li></ul></li>
<li> Garbage Collector:<ul>
    <li> Garbage Collector(GC)는 힙 메모리 영역에 생성된 객체들 중에서 참조되지 않은 객체들을 탐색 후 제거하는 역할</li>
    <li> 이때, GC가 역할을 하는 시간은 언제인지 정확히 알 수 없다.</li></ul></li>
<li> Runtime Data Area:<ul>
    <li> JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역</li></ul></li>
</details>
<details>
  <summary>1-1. JVM 동작 과정</summary>
  자바 컴파일러(javac)가 자바 소스코드(`.java`)를 읽어 자바 바이트코드(`.class`)로 변환시킵니다.<br>
  Class Loader를 통해 class 파일들을 JVM으로 로딩합니다.<br>
  로딩된 class파일들은 Execution Engine을 통해 해석됩니다.<br>
  해석된 바이트코드는 Runtime Data Areas에 배치되어 실질적인 수행이 이루어집니다.
</details>
<details>
  <summary>1-2. 자바의 메모리 영역에 대해 설명해주세요.</summary>
  자바의 메모리 공간은 크게 Method 영역, Stack 영역, Heap 영역으로 구분되고, 데이터 타입에 따라 할당됩니다.

<li> 메소드(Method) 영역 : 전역변수와 static 변수를 저장하며, Method 영역은 프로그램의 시작부터 종료까지 메모리에 남아있다.</li>
<li> 스택(Stack) 영역 : 지역변수와 매개변수 데이터 값이 저장되는 공간이며, 메소드가 호출될 때 메모리에 할당되고 종료되면 메모리가 해제된다. LIFO(Last In First Out) 구조를 갖고 변수에 새로운 데이터가 할당되면 이전 데이터는 지워진다.</li>
<li> 힙(Heap) 영역 : 프로그램 상에서 데이터를 저장하기 위해 런타임시 동적으로 할당하여 사용하는 메모리 영역으로 new 키워드로 생성되는 객체(인스턴스), 배열 등이 저장되된다.객체가  더 이상 쓰이지 않거나, 명시적으로 Null 선언시 GC 대상이 된다.</li>
</details>
<details>
  <summary>1-3. 각 메모리 영역이 할당되는 시점은 언제인가요?</summary>
  <li> Method 영역 : JVM이 동작해서 클래스가 로딩될 때 생성</li>
<li> Stack 영역 : 메소드가 호출될 때 할당</li>
<li> Heap 영역 : 런타임시 할당</li>
</details>
<details>
  <summary>1-4. JVM, JRE, JDK에 대해 설명해주세요.</summary>
  <li> JDK: 개발자들이 자바로 개발하는데 사용되는 SDK 키트, 자바를 개발할 때 필요한 라이브러리와 JRE가 포함</li>
<li> JRE: 자바 실행환경으로 JVM과 자바 프로그램을 실행시킬 때 필요한 라이브러리 API를 함께 묶어서 배포되는 패키지</li>
<li> JVM: 자바 가상머신으로 자바를 돌리는 프로그램, 자바 프로그램을 실행하기 위해서는 반드시 자바 가상 머신이 필요 (JRE에 포함)</li>
</details>

---

<details>
  <summary>2. GC가 무엇인가요?</summary>
  자바의 메모리 관리 방법으로 Heap 영역에서 동적으로 할당했던 메모리 중 필요 없게 된 메모리 객체를 모아 주기적으로 제거하는 프로세스
</details>
<details>
  <summary>2-1. GC의 동작 방식</summary>
  GC의 작업을 수행하기 위해 JVM이 어플리케이션의 실행을 잠시 멈추고, GC를 실행하는 쓰레드를 제외한 모든 쓰레드들의 작업을 중단 후 (Stop The World 과정) 사용하지 않는 메모리를 제거(Mark and Sweep 과정)하고 작업이 재개됩니다. GC의 작업은 Young 영역에 대한 Minor GC와 Old 영역에 대한 Major GC로 구분됩니다.
</details>
<details>
  <summary>2-2. 개발자가 메모리에 대해 신경을 덜 쓸 수 있어서 편해지는데, 그에 따른 단점은 없을까요?</summary>
  stop-the-world
    <li> GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것을 의미하는데, stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춥니다.</li>
    <li> GC 작업을 완료한 후 중단한 작업을 다시 시작합니다.</li>
    <li> 👉 GC 튜닝은 stop-the-world 시간을 줄이는 것을 의미합니다.</li>
</details>
<details>
  <summary>2-3. 개발자가 GC 튜닝을 하는 궁극적인 목표는 무엇일까요?제</summary>
  빠른 처리 속도를 달성하면서 stop-the-world의 최소화를 충족시키는 것이 목표입니다.
</details>

---

<details>
  <summary>3. 불변 객체가 무엇인지 설명하고 대표적인 Java의 예시를 설명해주세요.</summary>
  불변 객체는 객체 생성 이후 내부의 상태가 변하지 않는 객체를 말합니다. Java에서는 필드가 원시 타입인 경우 final 키워드를 사용해 불변 객체를 만들 수 있고, 참조 타입일 경우엔 추가적인 작업이 필요합니다.
</details>
<details>
  <summary>3-1. 참조 타입일 경우 추가적인 작업은 어떤게 있는지 설명해주세요.</summary>
  참조 타입은 대표적으로 1.객체를 참조할 수도 있고, 2.배열이나 3.List 등을 참조할 수 있습니다.

1. 참조 변수가 일반 객체인 경우 객체를 사용하는 필드의 참조 변수도 불변 객체로 변경해야 합니다.

2. 배열일 경우 배열을 받아 copy해서 저장하고, getter를 clone으로 반환하도록 하면 됩니다. (배열을 그대로 참조하거나, 반환할 경우 외부에서 내부 값을 변경할 수 있음. 때문에 clone을 반환해 외부에서 값 변경하지 못하게 함)

3. 리스트인 경우에도 배열과 마찬가지로 생성시 새로운 List를 만들어 값을 복사하도록 해야 합니다.배열과 리스트는 내부를 복사하여 전달하는데, 이를방어적 복사(defensive-copy)라고 합니다.
</details>
<details>
  <summary>3-2. 불변 객체나 final을 굳이 사용해야 하는 이유가 있을까요?</summary>

1. Thread-Safe하여 병렬 프로그래밍에 유용하며, 동기화를 고려하지 않아도 된다.(공유 자원이 불변이기 때문에 항상 동일한 값을 반환하기 때문)

2. 실패 원자적인 메소드를 만들 수 있다.(어떠한 예외가 발생되더라도 메소드 호출 전의 상태를 유지할 수 있어 예외 발생 전과 똑같은 상태로 다음 로직 처리 가능)

3. 부수효과를 피해 오류를 최소화 할 수 있다. ※ 부수효과 : 변수의 값이 바뀌거나 객체의 필드 값을 설정하거나 예외나 오류가 발생하여 실행이 중단되는 현상

4. 메소드 호출 시 파라미터 값이 변하지 않는다는 것을 보장할 수 있다.

5. 가비지 컬렉션 성능을 높일 수 있다.(가비지 컬렉터가 스캔하는 객체의 수가 줄기 때문에 GC 수행 시 지연시간도 줄어든다.)
</details>

---

<details>
  <summary>4. 자바의 모든 클래스는 Object 클래스를 상속받습니다. 그리고 Object클래스에는 equals() 와 hashCode() 라는 메소드가 선언되어 있습니다. 이 메소드들은 각각 어떤 역할일까요? 이 둘의 차이점은 무엇일까요?</summary>
  <li> equals()<ul>
    <li> 2개의 객체가 참조하는 것이 동일한지를 확인 👉 동일성(Identity)비교</li>
    <li> 즉, 2개의 객체가 가리키는 곳이 동일한 메모리 주소일 경우에만 동일한 객체가 된다.</li>
    <li> 하지만 프로그래밍을 하다보면 동일한 객체가 메모리 상에 여러 개 띄워져있는 경우가 있다. 해당 객체는 서로 다른 메모리에 띄워져있으므로 동일한(Identity) 객체가 아니다. 하지만 프로그래밍 상으로는 같은 값을 지니므로 같은 객체로 인식되어야 하는데, 이러한 동등성(Equality)을 위해 우리는 값으로 객체를 비교하도록 equals 메소드를 오버라이딩 해주는 것이다.</li></ul></li>
<li> hashCode()<ul>
    <li> 실행 중에(Runtime) 객체의 유일한 integer값을 반환한다.</li>
    <li> Object 클래스에서는 heap에 저장된 객체의 메모리 주소를 반환하도록 되어있다. (항상 그런 것은 아니다.)</li></ul></li>
</details>
<details>
  <summary>4-1. equals()와 hashCode()를 함께 override 해줘야 하는 이유는 무엇인가요?</summary>
  <li> `equals()`메서드를 오버라이딩하는 것은 메모리 주소가 다른 두 객체의 논리적 지위가 동일하다고 선언하는 것입니다.</li>
<li> 만약 `hashCode()`를 `equals()`와 함께 재정의하지 않으면 hash 값을 사용하는 Collection(HashSet, HashMap, HashTable)을 사용할 때 중복을 판단할 때 문제가 발생합니다.<ul>
    <li> HashTable(다른 Hash Collection 역시 동일)은 `<key, value>` 형태로 데이터를 저장합니다. 이 때 해시 함수를 이용해 키값 기준 고유 식별값인 해시값을 만듭니다. 이 해시값을 버킷에 저장합니다.</li>
    <li> 하지만 HashTable의 크기는 한정적이기 때문에 서로 다른 객체라 하더라도 같은 해시값을 가질 수 있습니다. (=> Hash Collisions; 해시충돌)</li>
    <li> 이처럼 같은 해시값의 버킷 안에 다른 객체가 있는 경우 `equals()`를 사용합니다.</li></ul></li>
<li> if) `hashCode()`를 재정의하지 않으면<ul>
    <li> 같은 값 객체라도 해시 값이 다를 수 있습니다. => HashTable에서 해당 객체가 저장된 버킷을 찾을 수 없습니다.</li></ul></li>
<li> if) `equals()`를 재정의하지 않으면<ul>
    <li> `hashCode()`가 만든 해시값을 이용해 객체가 저장된 버킷을 찾을 수는 있지만 해당 객체가 자신과 같은 객체인지 값을 비교할 수 없기 때문에 null을 리턴하게 됩니다.</li></ul></li>
</details>

---

<details>
  <summary>5. new String()과 리터럴("")의 차이에 대해 설명해주세요.</summary>
  new String()은 new 키워드로 새로운 객체를 생성하기 때문에 Heap 메모리 영역에 저장되고, ""는 Heap 안에 있는 String Constant Pool 영역에 저장됩니다.
</details>
<details>
  <summary>5-1. String 객체가 불변인 이유에 대해 아는대로 설명해주세요.</summary>
  
1. 캐싱 기능에 의한 메모리 절약과 속도 향상

- Java에서 String 객체들은 Heap의 String Pool 이라는 공간에 저장되는데, 참조하려는 문자열이 String Pool에 존재하는 경우 새로 생성하지 않고 Pool에 있는 객체를 사용하기 때문에 특정 문자열 값을 재사용하는 빈도가 높을 수록 상당한 성능 향상을 기대할 수 있다.

2. thread-safe

- String 객체는 불변이기 때문에 여러 쓰레드에서 동시에 특정 String 객체를 참조하더라도 안전하다.

3. 보안기능

- 중요한 데이터를 문자열로 다루는 경우 강제로 해당 참조에 대한 문자열 값을 바꾸는 것이 불가능하기 때문에 보안에 유리하다.
</details>

---
<details>
  <summary>6. 추상 클래스와 인터페이스의 차이</summary>
  <li>Interface:<ul>
    <li> 다중 상속 지원</li>
    <li> 추상 메서드만 가진다.</li>
    <li> 내부의 모든 필드는 public static final 상수</li>
    <li> abstract, default, private 제어자를 통해 구체적인 메서드를 가질 수 있다.</li>
    <li> 인터페이스는 클래스와 별도로 **구현 객체가 같은 동작을 한다는 것을 보장**하기 위해 사용하는 것에 초점</li></ul></li>
<li>abstract class:<ul>
    <li> 단일 상속만 가능</li>
    <li> 일반 클래스처럼 일반적인 필드, 메서드, 생성자를 가질 수 있음.</li>
    <li> 추상클래스는 클래스간의 연관 관계를 구축하는 것에 초점을 둔다.</li></ul></li>
</details>
<details>
  <summary>6-1. 인터페이스는 왜 사용하는가?</summary>
  인터페이스는 메서드의 틀을 미리 만들어 개발자 간의 의사소통 혼선을 줄여주고 다형성 개발에 유리함을 가져다주는 객체이다.
</details>

---

<details>
  <summary>7. Java의 stream에 대해 설명해주세요.</summary>
  Java 8부터 추가된 기술로 람다를 활용해 배열과 컬렉션을 함수형으로 간단하게 처리할 수 있는 기술이다.
</details>
<details>
  <summary>7-1. 스트림과 반복문의 차이가 무엇인지?</summary>
  1. 코드의 가독성<br>
스트림은 데이터 소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메소드를 정의해 놓아서 데이터 소스에 상관없이 모두 같은 방식으로 다룰 수 있으므로 코드의 재사용성이 높아진다.<br>
2. 병렬 처리 구현의 차이
<li>for: 구체적인 로직을 나누어 구현하고 합쳐야 합니다.</li>
<li>stream: parallelStream()으로 쉽게 처리됩니다.</li>
</details>

---
<details>
  <summary>8. 리플렉션(Reflection)이란 무엇인지 설명해주세요.</summary>
  리플렉션이란 구체적인 클래스 타입을 알지 못해도 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API 입니다.
</details>
<details>
  <summary>8-1. 리플렉션은 어떤 경우에 사용되는지 설명해주세요.</summary>
  코드를 작성할 시점에는 어떤 타입의 클래스를 사용할지 모르지만, 런타임 시점에 지금 실행되고 있는 클래스를 가져와서 실행해야 하는 경우 사용됩니다.<br>
프레임워크나 IDE에서 이런 동적인 바인딩을 이용한 기능을 제공합니다. intelliJ의 자동완성 기능, 스프링의 어노테이션이 리플렉션을 이용한 기능이라 할 수 있습니다.
</details>

---
<details>
  <summary>9. Java의 장단점</summary>
  <li> 장점<ul>
    <li> JVM 위에서 동작하기 때문에 운영체제에 독립적이다.</li>
    <li> 가비지컬렉터가 메모리를 관리해주기 때문에 편리하다.</li></ul></li>
<li> 단점<ul>
    <li> JVM 위에서 동작하기 때문에 실행 속도가 상대적으로 느리다.</li>
    <li> 다중 상속이나 타입에 엄격하는 등 제약이 많다.</li></ul></li>
</details>

---
<details>
  <summary>10. Java는 다중 상속을 지원합니까?</summary>
  아니요.
</details>
<details>
  <summary>10-1. Java가 다중 상속을 지원하지 않는 이유는 무엇입니까?</summary>
  다중 상속을 지원하면 다이아몬드 문제가 발생할 수 있기 때문입니다. 또한 구조 파악이 어렵습니다.

다이아몬드 문제: 예를 들어 Fruit 클래스에 있는 eat() 메서드를 Apple과 Banana 클래스가 각각 구현을 한 상황에서, Food라는 클래스가 Apple과 Banana를 다중 상속 받는다면 코드의 충돌이 발생하게 됩니다.
</details>

---
<details>
  <summary>11. 자바에서 동시성을 처리하는 방법에 대해 설명해주세요.</summary>
  <li> 스레드 동기화: 멀티스레드 환경에서 여러 스레드가 하나의 공유자원에 동시에 접근하지 못하도록 막는것을 말하며 synchronized라는 키워드를 통해 동기화한다.</li>
<li> 동시성 컬렉션 사용 e.g. ConcurrentHashMap, CopyOnWriteArrayList</li>
<li> CompletableFuture: CompletableFuture 클래스는 비동기 프로그래밍을 위한 기능을 제공합니다. 이를 사용하면 비동기 작업의 결과를 효율적으로 처리하고, 여러 비동기 작업을 조합하거나 연결할 수 있습니다.</li>
</details>

---
<details>
  <summary>12. Java의 StringBuffer와 StringBuilder 차이</summary>
  Java에서 StringBuffer와 StringBuilder는 모두 문자열을 다루기 위해 사용되지만, 주요 차이점은 동기화 여부에 있습니다.<br>
<li> StringBuffer는 동기화 지원 : 여러 스레드가 동시에 StringBuffer 객체를 수정하려고 할 때, 한 번에 하나의 스레드만 변경할 수 있도록 한다. 그래서 StringBuilder보다 느릴 수 있다.</li>
<li> StringBuillder는 동기화 지원 X: 따라서 멀티스레드 환경에서 안전하지 않을 수 있지만, 빠르다!</li>
</details>

---
<details>
  <summary>13. OOME(Out of Memory Error)란?</summary>
  객체를 생성하는 과정에서 힙 공간에 객체를 할당하기 위한 공간이 부족할 경우 발생한다.
</details>
<details>
  <summary>13-1. OOME의 종류와 원인, 해결법에 대해 설명해주세요</summary>
  <li> java.lang.OutOfMemoryError: Java heap space(Java 힙 공간)<ul>
    <li> 원인<ul>
        <li> 자바 힙 공간에 새로운 객체를 생성할 수 없는 경우에 발생한다.</li>
        <li> 메모리 누수가 아닌 지정한 힙 크기(혹은 기본 크기)가 애플리케이션에 충분하지 않은 경우에도 발생한다.</li>
        <li> 혹은, 생명주기가 긴 애플리케이션의 경우 finalize를 과도하게 사용할 때 발생하기도 한다.<ul>
            <li> finalize는 소멸을 명시적으로 할 때 사용하나 GC에 마킹하는 데 오래걸리는 단점이 있다.</li></ul></li>
        </ul></li>
    <li> 조치<ul>
        <li> JVM Option 을 통해 Heap size 를 늘려 해결할 수 있다.</li></ul></li></ul></li>
<li> java.lang.OutOfMemoryError: GC Overhead limit exceeded(GC 오버헤드 한도 초과)<ul>
    <li> 원인<ul>
        <li> 메모리가 부족하여 가비지 컬렉션이 이루어졌지만, 새로 확보된 메모리가 전체 메모리의 2% 미만일 때 발생한다.</li>
        <li> 더 이상 가비지 컬렉션을 할 수 없을 정도로 메모리를 사용한다는 것이다.</li></ul></li>
    <li> 조치<ul>
        <li> 힙 크기를 늘린다.</li>
        <li> XX:-UseGCOverheadLimit 선택사항을 추가하여 java.lang.OutOfMemoryError가 발생하는 초과 오버헤드 GC 제한 명령을 해제할 수 있다.</li></ul></li></ul></li>
</details>

---
<details>
  <summary>14. Inner Class란 무엇인가요?</summary>
  하나의클래스 내부에 선언된 또 다른 클래스를 말합니다.
</details>
<details>
  <summary>14-1. Inner Class(내부 클래스)의 장점에 대해 설명해주세요.</summary>
  만약 해당 클래스가 하나의 클래스하고만 관계를 맺는 경우, 이너클래스로 작성하는 것이 유지보수 면이나 코드의 이해성 면에서 편리해집니다.

또한 더욱 타이트한 캡슐화 적용이 가능해집니다. 캡슐화를 통해 외부에서의 접근을 차단하면서도, 내부 클래스에서 외부 클래스의 멤버들을 제약 없이 쉽게 접근할 수 있어 구조적인 프로그래밍이 가능해집니다. 또한 클래스 구조를 숨김으로써 코드의 복잡성도 줄일 수 있습니다.
</details>
<details>
  <summary>14-2. 이너 클래스 사용한 적 있으신가요? 언제 사용하셨나요?</summary>
  내용
</details>

---
<details>
  <summary>15. 자바의 static 키워드에 대해 설명해주세요.</summary>
  Java에서 Static 키워드를 사용한다는 것은 메모리에 한번 할당되어 프로그램이 종료될 때 해제되는 것을 의미합니다.
</details>
<details>
  <summary>15-1. static function의 특징에 대해 설명해주세요</summary>
  static 메모리 영역에 존재하므로 객체가 생성되기 이전에 이미 할당이 되어 있습니다. 그렇기 때문에 객체의 생성없이 호출하여 사용할 수 있습니다.

주로 유틸성 함수에 사용됩니다.
</details>
<details>
  <summary>15-2. 단점이 있나요?</summary>
  static 키워드가 붙은 변수나 함수는 자바의 메모리 영역에서 static 메모리에 위치하게 됩니다. static 영역은 Garbage Collector의 영역 밖이기 때문에 static을 자주 사용한다면 메모리 효율성을 떨어뜨리게 됩니다.
</details>

---
<details>
  <summary>16. 가비지 컬렉터(GC)란?</summary>
  '더이상 참조되지 않는 메모리'인 가비지를 청소해주는 JVM의 실행 엔진의 한 요소입니다. JVM은 new와 같은 연산에 의해 새롭게 생성된 객체들 중에서 더이상 참조되지 않는 객체를 정리해줍니다. 가비지 컬렉터는 Heap 영역을 위주로 탐색하며 메모리를 정리해줍니다.
</details>
<details>
  <summary>16-1. GC의 단점은?</summary>
  stop-the-world: GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것을 의미하는데, stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춥니다.
</details>
<details>
  <summary>16-2. 가비지 컬렉션(Garbage Collection)에 의한 시스템 중단 시간을 줄이는 방법</summary>
  <li> 옵션을 변경하여 GC의 성능을 높이기<ul>
    <li> young 영역과 old 영역의 힙 크기를 높여 GC의 빈도를 줄이는 것</li>
    <li> 객체의 할당과 promotion을 줄이는 것</li></ul></li>
<li> 설정을 변경하여 GC의 성능을 높이기<ul>
    <li> 애플리케이션을 중단시킨 후에 GC를 병렬로 동시에 진행시키는 것</li>
    <li> 애플리케이션과 GC작업을 동시에(concurrent) 진행시키는 것</li></ul></li>
<li> 개발자의 코드를 변경하여 GC의 성능을 높이기<ul>
    <li> Collection 등을 활용할 때 사용할 객체의 크기를 명시해주기</li>
    <li> 스트림을 바로 사용하기<ul>
        <li> 변경 전: byte[] fileData = readFileToByteArray(new File("myfile.txt"));</li>
        <li> 변경 후: FileInputStream fis = new FileInputStream(fileName);</li></ul></li>
    <li> 불변(Immutable) 객체 사용하기</li></ul></li>
</details>

---