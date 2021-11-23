> 망나니 개발자님의 [티스토리](https://mangkyu.tistory.com) 글을 읽고 정리하였습니다. 



## Spring Bean이란?

스프링 IoC 컨테이너가 관리하는 자바 객체를 빈(Bean)이라고 한다. Bean은 Spring IoC 컨테이너에 의하여 생성되고 관리된다.



## Spring Bean 구성요소

- class: Bean으로 등록할 자바 클래스
- id: Bean의 고유 식별자
- scope: Bean을 생성하기 위한 방법(singleton, prototype 등)
  - spring은 기본적으로 Singleton방식으로 빈이 생성된다.
    - 싱글톤은 여러 번 빈을 요청하더라도 매번 동일한 객체를 돌려준다.
    - 따라서 매번 클라이언트의 요청이 올 때마다 각 로직을 처리하는 빈을 새로 만들 필요가 없으므로 대규모 트래픽을 처리하기에 유리하다.
    - 빈을 싱글톤 스코프로 관리하면 요청이 왔을 때 여러 개의 스레드가 빈을 공유해 처리한다.
  - Bean Scope 종류
    - 싱글톤: Spring 프레임워크에서 기본으로 채택하는 스코프로, 스프링 컨테이너의 시작부터 종료까지 1개의 객체로 유지된다.
    - 프로토타입: 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는다. 그 후는 클라이언트가 해당 객체들을 관리해야 한다.
    - request: HTTP request의 생명주기 안에 단 하나의 객체만 존재한다. 각각의 요청이 들어오고 나갈 때까지 유지
    - session: HTTP session의 생명주기 안에 단 하나의 객체만 존재한다. 각각의 세션이 생성되고 종료될 때까지 유지
- constructor-arg: Bean 생성 시 전달할 파라미터
- property: Bean 생성 시 setter에 전달할 인수



## @Bean, @Configuration, @Component

- @Bean
  - 개발자가 직접 제어가 불가능한 외부 라이브러리 또는 설정을 위한 클래스를 Bean으로 등록할 때 @Bean 어노테이션을 활용한다.
- @Configuration
  - 1개 이상의 @Bean을 제공하는 클래스의 경우 반드시 @Configuration을 명시해 주어야 한다.
- @Component
  - 개발자가 직접 개발한 클래스를 Bean으로 등록하고자 하는 경우 @Component 어노테이션을 활용한다.



## IoC Container vs Bean Factory vs Application Context

스프링에서 Bean의 생성과 관계 설정을 담당하는 IoC 컨테이너를 Bean Factory라고 한다. 하지만 실제로는 빈의 생성과 관계 설정 외에 추가적인 기능이 필요한데, 이러한 이유로 Spring에서는 Bean Factory를 상속하여 확장한 Application Context를 사용한다.



## Application Context

어플리케이션 컨텍스트는 별도의 설정 정보를 참고하고 IoC를 적용하여 빈의 생성, 관계 설정 등의 제어 작업을 총괄한다. 즉, 생성 정보와 연관관계 정보에 대한 설정을 읽어 처리한다. 대표적인 IoC의 설정정보로 @Configuration이 있다.



## Application Context의 장점

- 클라이언트는 @Configuration이 붙은 구체적인 팩토리 클래스를 알 필요가 없다.
  - 어플리케이션이 발전하면 팩토리 클래스가 계속해서 증가할텐데, 애플리케이션 컨텍스트가 없다면 클라이언트는 원하는 객체를 가져오기 위해 어떤 팩토리 클래스에 접근해야 하는지 알아야 하는 번거로움이 생긴다. 반면에 애플리케이션 컨텍스트를 사용하면 팩토리가 아무리 많아져도 이에 직접 접근할 필요가 없어 일관된 방식으로 원하는 빈을 가져올 수 있따.
- 종합 IoC 서비스를 제공한다.
  - Bean 객체가 만들어지는 방식과 시점등을 다르게 가져갈 수 있고 그 외에도 후처리나 정보의 조합 인터셉트등 다양한 종합 서비스를 제공한다.
- 다양한 빈 검색 서비스를 제공한다.
  - 애플리케이션 컨텍스트에서 빈 목록을 관리하여 빈 이름이나 타입 또는 어노테이션 설정 등으로 빈을 찾을 수 있다.





## 참고

https://mangkyu.tistory.com/5?category=761302

