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
