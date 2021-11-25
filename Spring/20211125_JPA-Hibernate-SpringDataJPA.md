> [티스토리 글](https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/)을 읽고 정리하였습니다. 



JPA, Hibernate, Spring Data JPA 개념을 명확히 구분해보자.



## JPA

JPA(Java Persistence API)는 기술 명세이며, 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스다. 인터페이스이기 때문에 어떠한 기능을 하는 라이브러리가 아니다. 



## Hibernate

Hibernate는 JPA라는 명세의 구현체이다. JPA는 interface고, Hibernate는 JPA를 implement한 class로 비유할 수 있겠다.

Hibernate는 JPA를 구현한 구현체이기 때문에 JPA를 사용하기 위해서 반드시 Hibernate를 사용할 필요는 없다. Hibernate의 작동 방식이 맘에 들지 않는다면 다른 구현체를 사용해도 되고, 심지어 직접 구현해서 사용할 수도 있다. 그러지 않는 이유는 Hibernate가 충분히 성숙한 구현체이기 때문이다.



## Spring Data JPA

Spring Data JPA는 JPA를 편한하게 사용할 수 있도록 만들어놓은 모듈이다. 이는 JPA를 한 단계 더 추상화시킨 Repository 인터페이스를 제공하며 이루어진다. **사용자가 Repository 인터페이스에서 정해진 규칙대로 메소드를 입력하면, Spring이 알아서 해당 메소드 이름에 적합한 쿼리를 날리는 구현체를 만들어서 Bean으로 등록해준다.**

여기서 Spring Data JPA가 JPA를 추상화했다는 말은, Spring Data JPA의 Repository의 구현에서 JPA를 사용하고 있다는 것이다.

또한 Spring Data JPA는 항상 하이버네이트와 같은 JPA provider가 필요하다.


