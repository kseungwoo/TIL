> 김영한님의 [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/) 강의를 듣고 정리하였습니다. 
>




## URI (Uniform Resource Identifier)

**URI**는 리소스를 식별하는 문자열이다.

인터넷의 우편물 주소 같은 것으로, 정보 리소스를 고유하게 식별하고 위치를 지정할 수 있다.

- **U**niform: 리소스 식별하는 통일된 방식
- **R**esource: 자원, URI로 식별할 수 있는 모든 것 (제한 없음)
- **I**dentifier: 다른 항목과 구분하는데 필요한 정보 



### URI, URL, URN의 관계

<img src="https://user-images.githubusercontent.com/71204049/135708577-447850a2-389a-4078-ab6d-ed7c2c2a49a0.png" width="450" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))

URI는 **로케이터(Locator), 이름(Name) 또는 두 가지 모두로 분류**될 수 있다.



<img src="https://user-images.githubusercontent.com/71204049/135708714-8343b899-4a4f-4e22-90e6-7aa443547b16.png" width="600" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))



URL은 리소스가 있는 **위치를 지정** (Locator)

URN은 리소스에 **이름을 부여** (Name)

위치는 변할 수 있지만 이름은 변하지 않는다.

URN만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않았다.

URI는 주로 URL과 같은 의미로 쓰인다.



## URL 문법 예시

- scheme://{userinfo@}host{:port}{/path}{?query}
- https://www.google.com:443/search?q=uri&hl=ko
  - 프로토콜(https)
  - 호스트명(www.google.com)
  - 포트 번호(443)
  - 경로(/search)
  - 쿼리 파라미터(q=hello&hl=ko)



#### <u>scheme</u>

- 주로 프로토콜 사용
  - 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 규칙 (ex. http, https, ftp 등)
- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
  - https는 http에 보안 추가 (HTTP Secure)

#### <u>userinfo</u>

- URL에 사용자 정보를 포함해서 인증
- 거의 사용하지 않음

#### <u>host</u>

- 호스트명
- 도메인명 또는 IP 주소를 직접 사용가능

#### <u>port</u>

- 접속 포트
- 일반적으로 생략, 생략시 http는 80, https는 443

#### <u>path</u>

- 리소스 경로(path), 계층적 구조

#### <u>query</u>

- key=value 형태
- ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

#### <u>fragment</u>

- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아님



## 웹 브라우저 요청 흐름

<img src="https://user-images.githubusercontent.com/71204049/135709714-55925925-fe9a-4757-8af2-e8329cc8695e.png" width="600" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))



- DNS 조회 -> IP 정보 확인
- PORT 확인
- HTTP 요청 메시지 생성



**HTTP 요청 메시지 (예시)**

```
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```



**HTTP 메시지 전송 과정**

<img src="https://user-images.githubusercontent.com/71204049/135709926-d458f280-bc17-40a3-82fe-82dd9caccea8.png" width="600" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))



**HTTP 응답 메시지 (예시)**

```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
  <body>...</body>
</html>
```

웹 브라우저는 응답받은 메시지의 HTML을 렌더링한다.
