<details>
  <summary>1. BeanScope 란 무엇이고 어떤 것들이 있나요?</summary>
  빈이 존재할 수 있는 범위를 뜻하며 싱글톤, 프로토타입, 웹 관련 스코프가 있습니다. 스프링 빈은 기본적으로 싱글톤 스코프로 생성됩니다.
</details>
<details>
  <summary>1-1. 각각 어떤 Scope 를 갖나요?</summary>
  1. 싱글톤: 기본 스코프로, 스프링 컨테이너의 시작과 종료까지 유지<br>
  2. 프로토타입: 스프링 컨테이너는 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않음 프로토타입 스코프 빈을 스프링 컨테이너에 조회하면 스프링 컨테이너는 항상 새로운 인스턴스를 생성해서 반환<br>
  3. 웹 관련 스코프

    request : 웹 요청이 들어오고 나갈때 까지 유지
    session : 웹 세션이 생성되고 종료될때까지 유지
    application : 웹의 서블릿 컨텍스트와 같은 범위로 유지
</details>

---

<details>
  <summary>2. Spring 에서 핵심 기능을 무엇이라고 생각하시나요?</summary>
    스프링의 핵심 기능에는 DI, IoC, AOP, MVC 가 있습니다.
</details>
<details>
  <summary>2-1. 각각 어떤 것인지 간략하게 설명해주세요.</summary>
    1. DI: 의존성 주입이란 객체 간의 의존 관계를 객체 자신이 아닌 외부에서 주입하는 것입니다.<br>
    2. IoC: 제어의 역전이란 객체의 생성, 생명주기의 관리를 외부 컨테이너가 담당하는 것입니다.<br>
    3. AOP: 관점 지향 프로그래밍이란 핵심 비즈니스 로직과 공통 모듈을 분리하여 관리하는 것입니다.<br>
    4. MVC: Model, View, Controller 로 나누어 사용자 인터페이스와 비즈니스 로직을 분리하는 것입니다.
</details>

---

<details>
  <summary>3. DI 란 무엇인가요?</summary>
  의존성 주입을 의미하며 객체들 간의 의존 관계를 설정하는 것입니다.
</details>
<details>
  <summary>3-1. DI 방식에는 어떤 것들이 있나요?</summary>
  setter 주입, 생성자 주입, 필드 주입이 있습니다.
</details>
<details>
  <summary>3-2. 여러 DI 방식들 중에 생성자 주입이 가장 많이 사용되는 이유를 무엇이라고 생각하나요?</summary>
  final 키워드를 사용하여 객체의 불변을 보장할 수 있고, 개발자의 실수로 인해 빈 주입이 이루어지지 않았을 경우 컴파일 시점에서 오류를 확인할 수 있기 때문입니다. 
</details>

---

<details>
  <summary>4. Spring Bean 이란 무엇인가요?</summary>
  스프링 컨테이너에서 생성되고 관리되는 객체입니다.
</details>
<details>
  <summary>4-1. Spring Bean 을 등록하는 방법에 대해 설명해주세요.</summary>
  Spring Bean 을 등록하는 방법에는 Configuration 애노테이션을 사용하여 설정파일을 통해 등록하는 방법과 컴포넌트 스캔을 통해 등록하는 방법이 있습니다.
</details>
<details>
  <summary>4-2. 컴포넌트 스캔은 어떤식으로 동작하나요?</summary>
  스프링 컨테이너가 띄워 질 때 자바 실행 파일이 존재하는 패키지 하위의 @Component 를 가진 클래스들을 스캔하여 스프링 빈으로 등록합니다. @Controller, @Service, @Repository 은 @Component 를 포함하고 있어 컴포넌트 스캔의 대상이 됩니다.
</details>
<details>
  <summary>4-3. 그렇다면 Controller, Service, Repository 애노테이션은 어떤 역할을 하나요?</summary>
  @Controller : 스프링 MVC 컨트롤러로 인식<br>
  @Service : 스프링 비지니스 로직에서 사용 특별한 처리가 따로 없고 비지니스 계층을 인식하는데 도움이 됨<br>
  @Repository : 스프링 데이터 접근 계층에서 사용 데이터 계층에서 발생하는 예외를 스프링이 추상화하여 서비스 계층에서 추상화된 예외에 의존하도록 해줌
</details>

---

<details>
  <summary>5. JPA 에서 지연 로딩이란 무엇이고 왜 사용하는 건지 설명해주세요.</summary>
    지연로딩은 연관관계가 설정된 엔티티를 조회할 때 연관된 엔티티를 조회하지 않고, 실제로 사용될 때 조회하는 것을 의미합니다. 연관관계가 설정된 엔티티를 조회할 때 연관된 엔티티를 조회하지 않고, 실제로 사용될 때 조회하므로 성능상의 이점이 있습니다.
</details>
<details>
  <summary>5-1. JPA 에서는 지연 로딩을 어떤 방법으로 제공하는지 설명해주세요.</summary>
    JPA 에서는 지연 로딩을 프록시 객체를 통해 제공합니다. 프록시 객체는 실제 객체를 대신하여 사용되며, 실제 객체가 사용될 때 초기화되어 사용됩니다.
</details>
<details>
  <summary>5-2. oneToOne 연관관계에서 지연 로딩을 할 수 없는 경우에 대해 알고 계신가요?</summary>
  oneToOne 연관관계에서 연관관계의 주인이 아닌 쪽에서 조회를 할 경우 지연 로딩이 불가능합니다. 연관 관계의 주인이 아닌 쪽에서 조회를 할 경우 외래키를 조회할 수 없기 때문입니다.
</details>

---

<details>
  <summary>6. 영속성 전이랑 무엇인가요?</summary>
  특정 엔티티를 영속 상태로 만들 때 연관된 엔티티로 함께 영속 상태로 만드는 것을 의미합니다.
</details>
<details>
  <summary>6-1. 고아객체란 무엇인가요?</summary>
  부모 엔티티의 참조가 끊어진 자식 엔티티를 의미합니다.
</details>
<details>
  <summary>6-2. JPA 에서 CascadeType 을 REMOVE 로 하는 것과 orphanRemoval 을 True 로 하는 것의 차이가 무엇인가요?</summary>
    CascadeType 을 Delete 로 설정하면 부모 엔티티를 삭제할 때 자식 엔티티도 함께 삭제됩니다. orphanRemoval 을 True 로 설정하면 부모 엔티티와 연관관계가 끊어진 자식 엔티티를 삭제합니다.
</details>

---

<details>
  <summary>7. JPA 에서 영속성 컨텍스트란 무엇인가요?</summary>
  엔티티를 영구 저장하는 환경으로 영속성 컨텍스트에 속한 엔티티들은 JPA 가 관리합니다. 엔티티 메니저를 통해 영속성 컨텍스트에 접근할 수 있습니다.
</details>
<details>
  <summary>7-1. JPA 엔티티의 생명주기에 대해 설명해주세요.</summary>
  비영속 상태 -> 영속 상태 -> 준영속 상태 or 제거 상태
  - 비영속 상태: 영속성 컨텍스트와 전혀 관계가 없는 상태로 일반 자바 객체
  - 영속 상태: 영속성 컨텍스트에서 관리되는 객체. 해당 객체는 flush 전까지 영속성 컨텍스트에만 존재하다가 flush 가 되면 db 에 영속화 됨
  - 준영속 상태: 영속성 컨텍스트에 저장되었다가 분리된 상태
  - 제거 상태: 영속성 컨텍스트에서 제거된 상태
</details>
<details>
  <summary>7-2. 영속성을 갖는 엔티티는 일반 객체와 어떤 차이가 있나요?</summary>
  - 1차 캐시에 저장: PK 를 키로 하는 1차 캐시에 저장. PK 로 조회할 경우 db 를 조회하지 않고 1차 캐시에 있는 엔티티를 반환
  - 동일성 보장: 영속성 컨텍스트는 1차 캐시에 있는 인스턴스를 반환하므로 동일성 보장
  - 쓰기 지연: persis 를 할 때, 쿼리를 db 에 바로 전달하지 않고 1차 캐시에 저장하고 쓰기 지연 SQL 저장소에 저장. 트랜잭션이 커밋되거나 flush 되면 쓰기 지연 SQL 저장소에 쌓여있던 쿼리들을 db 에 전달
  - 변경 감지: jpa 는 영속성 컨텍스트에 엔티티의 최조 상태인 스냅샷을 저장. flush 가 호출되면 현재의 엔티티와 스냅샷을 비교하여 update sql 을 쓰기 지연 SQL 저장소에 추가
</details>
<details>
  <summary>7-3. flush 와 commit 의 차이가 무엇인가요?</summary>
    flush 는 영속성 컨텍스트의 변경 내용을 데이터베이스에 동기화하는 작업을 의미하며 commit 은 트랜잭션의 변경 내용을 데이터베이스에 영구적으로 반영하는 작업을 의미합니다.
</details>

---

<details>
  <summary>8. 테스트에서 모킹이란 무엇인가요?</summary>
  테스트에서 외부 의존성을 가짜 객체로 대체하는 것을 의미합니다.
</details>
<details>
  <summary>8-1. 모킹을 사용하는 이유가 무엇인가요?</summary>
  테스트하고자 하는 객체가 의존하는 외부 객체가 있을 때, 외부 객체의 동작을 제어하거나 특정 상황을 시뮬레이션 하기 위해 사용합니다.
</details>
<details>
  <summary>8-2. 모킹의 단점을 무엇이라고 생각하나요?</summary>
    실제 객체와 다르게 동작할 수 있습니다. 또한, 모킹을 남발하게 되면 테스트 코드가 복잡해질 수 있습니다.
</details>

---

<details>
  <summary>8. DataJpaTest 애노테이션이 무엇인지 설명해주세요.</summary>
    JPA 컴포넌트들을 테스트하기 위한 애노테이션입니다. 전체 컴포넌트가 아닌 JPA 와 관련된 컴포넌트들만 빈을 등록합니다. 또한 트랜잭션 애노테이션을 포함하며 테스트가 끝나면 롤백합니다.
</details>
<details>
  <summary>8-1. SpringBootTest 애노테이션으로도 테스트할 수 있는데 DataJpaTest 애노테이션을 사용하여 테스트하는 이유가 무엇인가요?</summary>
    SpringBootTest 애노테이션은 전체 컴포넌트를 빈으로 등록하기 때문에 테스트 시간이 오래 걸릴 수 있습니다. DataJpaTest 애노테이션은 JPA 와 관련된 컴포넌트들만 빈으로 등록하기 때문에 테스트 시간을 단축할 수 있습니다.
</details>
<details>
  <summary>8-2. 그렇다면 JPA 와 관련된 컴포넌트들에는 뭐가 있나요?</summary>
    JPA 레포지토리, 엔티티, EntityManager 등이 있습니다.
</details>
