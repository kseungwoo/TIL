## REST란

<img src="https://user-images.githubusercontent.com/71204049/142902896-bc06fd5c-a564-4884-adb4-e28dca8dab7b.png" width="800" />

(사진 출처: [티스토리](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html))

**REST(Representational State Transfer)**란, 자원을 이름으로 구분하며 자원의 상태(정보)를 주고 받는 일련의 과정을 의미한다.

구체적으로는, HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.



- 자원을 이름으로 구분
  - DB의 계좌 정보가 자원일 때, 이 자원의 이름(표현)을 accounts로 정한다.- 

- 상태(정보) 전달
  - 데이터가 요청되어지는 시점에서 자원의 상태를 전달한다.
  - 일반적으로 JSON 또는 XML을 통해 주고 받는 것이 일반적이다. (XML을 JSON이 대체하는 추세)
    - JSON: key:value 쌍들로 이루어진 object 형태이고, 서버와 클라이언트 사이의 통신에서 데이터 교환 포맷으로 많이 사용된다.
    - XML: 데이터를 태그로 감싼 형태. JSON보다 데이터 처리 속도가 느림.



## REST의 구성 요소

- 구성 요소
  - 자원(Resource) : URI
    - 클라이언트는 URI를 통해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 서버에 요청한다.
  - 행위(Verb) : HTTP Method
    - HTTP Method: Get, PUT, POST, DELETE와 같은 메서드
  - 표현(Representation of Resource) : JSON or XML
    - REST에서 하나의 자원은 JSON, XML등의 여러 형태의 데이터로서 표현이 되며 이를 주고 받는다.

## REST 장단점

**장점**

- HTTP 표준 프로토콜을 따르는 모든 플랫폼에서 사용이 가능하다.
  - RESTful하게 설계한 api 서버는 http 표준 프로토콜을 사용하는 다양한 클라이언트(디바이스)와 통신할 수 있다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도를 더 쉽게 파악할 수 있다.
- REST 기반으로 시스템을 분산할 경우 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.

**단점**

- HTTP Method 형태가 제한적이다.
- 구형 브라우저가 아직 제대로 지원하지 못하는 부분이 존재한다.





## REST 특징

1. Server - Client 구조
   - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client
     - Server: API를 제공하고 비즈니스 로직 처리 및 자원 저장을 책임진다.
     - Client: 사용자 인증이나 세션 및 로그인 정보 등의 context를 책임진다.
   - 역할이 명확하게 구분되어 서로 간의 의존성이 줄어든다.
2. Stateless(무상태성)
   - HTTP가 Stateless하기 때문에 REST 역시 무상태성을 갖는다.
   - Client의 Context(세션 및 로그인 정보 등)를 서버에 저장하지 않는다.
   - Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
     - Server의 처리 방식에 일관성
3. Cacheable (캐시 가능)
   - HTTP 프로토콜 위에서 동작하기 때문에 HTTP가 가진 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
   - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
   - 캐시 사용을 통해 사용자에 대한 응답 시간이 빨라지고 서버의 자원 이용률, 성능 등을 향상시킬 수 있다.

4. Layered System (계층형 구조)
   - REST Server는 다중 계층으로 구성될 수 있다.
   - Client는 REST API Server만 호출한다.
   - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
   - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
5. Uniform Interface(인터페이스 일관성)
   - 특정 언어나 기술에 종속되지 않고, HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.





## API

**API(Application Programming Interface)**는 시스템 간에 서로 상호 작용하여 원하는 데이터를 CRUD하거나 특정 기능을 수행하고자 할 때 이 요청을 시스템에 전달하고 성공적으로 응답을 수행할 수 있도록 지원한다. 즉 정보의 교환을 가능하게 하는 것이다.



## REST API란

REST를 기반으로 구현한 API이다.



## REST API 설계 규칙

1. 대문자보다는 소문자를 사용한다.
2. 단수형보다는 복수형을 사용한다.
3. 언더바(_)대신 하이픈(-)을 사용한다.
4. URI의 마지막에는 슬래시(/)를 포함하지 않는다.
5. 계층관계를 나타낼 때 슬래시(/)를 사용한다.
6. 전달하고자 하는 자원의 명사를 사용하되 컨트롤 자원일 경우 예외적으로 동사를 허용한다.
7. 파일 확장자는 URI에 포함하지 않는다.



## RESTful이란

REST 원리를 잘 따르는 시스템을 보통 RESTful하다고 표현한다. REST API를 제공하는 서비스 또한 RESTful하다고 볼 수 있다.





## 참고

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

https://velog.io/@pjh612/REST-API-URI-%EA%B7%9C%EC%B9%99
