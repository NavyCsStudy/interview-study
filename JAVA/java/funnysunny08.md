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
