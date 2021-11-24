현재 개발 중인 얼리버디 앱의 인증 서버를 정비하고 있다.

Zeplin에서 UI를 확인하니 자체 회원가입을 통한 로그인과 소셜 로그인 방식(네이버, 구글, 카카오) 모두 구현되어있었다. 우선 순위는 낮지만 OAuth2.0의 도입을 고려해야했다.

따라서 JWT와 OAuth에 대한 추가적인 학습이 필요했다. 이 글은 OAuth와 JWT에 대해 조사하고 필요한 자료를 취합하며 앞으로 인증 관련 서버 개발 방향성에 대해 고민한 흔적이다. 



## OAuth

- OAuth(Open Authentication 또는 Open Authorization)는 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 **개방형 표준**이다

- OAuth의 기본 핵심은 인증 과정을 제 3자에게 위임하는 것이다. 따라서 제 3자의 인증 정보를 내 서비스에서 이용한다고 볼 수 있다. 여기서 제 3자에는 카카오, 구글 등이 있다.

- OAuth가 사용되기 전에는  외부 사이트와 인증 기반의 데이터를 연동할 때 인증 방식의 표준이 없었기 때문에 기존의 기본 인증인 아이디와 비밀번호를  사용했는데, 이는 보안상 비밀번호 노출에 취약한 구조였다. 그렇기 때문에 이 문제를 보안하기 위해 OAuth의 인증은 API를 제공하는 서버에서 진행하고, 유저가 인증되었다는 Access Token을 발급하였다. 그 발급된 Access token으로 Third party(Consumer) 애플리케이션에서는 Service Provider의 API를 안전하고 쉽게 사용할 수 있게 되었다.

  출처: https://minwan1.github.io/2018/02/24/2018-02-24-OAuth/



## OAuth 2.0

- OAuth 1.0을 개선하여 나온 최신 기술
- Oauth 1.0은 HTTPS가 필수가 아니어서 signature를 따로 생성해서 호출해야 했지만, OAuth 2.0은 Bearer 토큰 인증 방식으로  간편화하였다.
  - Bearer: JWT 또는 OAuth에서 사용하는 토큰 인증 타입.
- Authorization Server를 분리함으로써 인증 서버를 확장할 수 있다.



## OAuth 2.0 Roles

- Resource Owner
  - 앱을 사용하는 사용자다. 앱에 보호된 리소스에 대한 접근 권한을 부여한다. 
- Client
  - OAuth 인증 방식을 채택한 애플리케이션이다. 
- Authorization Server
  - Resource Owner를 인증하고, 권한을 얻으면 Client에게 Access Token을 발급하는 서버
- Resource Server
  - Access Token을 통해 보호된 리소스에 대한 Client의 요청을 수락하고 그 리소스를 응답에 담아 보내주는 서버
- 네이버나 구글 OAuth 2.0 서비스를 사용하면 ResouceServer, Authorization Server는 네이버, 구글이 되고 Client는 개발하는 애플리케이션이며 Resource Owner는 그것을 사용하는 사용자이다.

출처: https://sun-22.tistory.com/44



## Abstract OAuth2.0 Protocol Flow

<img src="https://user-images.githubusercontent.com/71204049/143189691-4876df9f-c7fb-45a8-b287-1d36941320ac.png" width="500" />

(A): Client는 Resource Owner에 권한(Authorization)을 요청한다. 이 승인은 직접적으로 혹은 Authorization Server를 통해 간접적으로 이루어질 수 있다.

(B): Resource Owner가 권한을 부여했을 시 Client는 Authorization Grant(권한 증서)를 받는다. Authorization Grant 방식은 다양하며 클라이언트의 요청이나 인증 서버가 지원하는 유형에 따라 달라질 수 있다.

(C): Client는 인증서버에 Authorization Server에 인증과 권한 증서를 제시함으로써 Access Token을 요청한다.

(D): Authorization Server는 Client를 검증하고 권한 증서가 유효하면 Access Token을 발급한다.

(E): Client는 Access Token을 제시함으로써 Resource Server에 보호된 리소스를 요청한다

(F): Resource Server는 Access Token을 검증하고 검증되었다면 Client에게 보호된 리소스를 전송한다.

출처: https://sun-22.tistory.com/44



## OAuth 2.0 4가지 인증방식

1. Authorization Code Grant

2. Implicit Grant

3. Resource Owner Password Credentials Grant

4. Client Credentials Grant

웹이나 앱에서는 Authorization Code Grant 방식이 가장 많이 사용된다. 따라서 Authorization Code Grant 방식을 채택한다는 가정하에 아래 설명을 서술할 것이다.



## JWT란

JWT(Json Web Token)은 JSON 객체를 사용하여 가볍고 self-contained 방식으로 정보를 안정적으로 전달해주는 방식이다.

Self-contained는 필요한 모든 정보를 자체적으로 가지고 있다는 뜻으로, 토큰에 대한 기본 정보, 전달할 유저 정보, 토큰 검증 유에 대한 정보 등을 포함하고 있다.

유저가 서버에 요청할 때 헤더에 JWT를 포함에 전달하면 서버는 그 토큰을 검증하고 권한을 처리한다. 

- 장점
  - 따로 세션(서버에 저장하는 활성화된 접속 정보)을 유지할 필요가 없다. (Stateless)
  - 쿠키를 전달하지 않아도 되므로 쿠키를 사용함으로써 발생하는 취약점이 사라진다.
  - 요청 받은 토큰만 검증하면 되므로 추가적인 인증을 위한 DB Storage에 대한 I/O 작업 없이 서버 자원을 아낄 수 있다.
    - 사용자 인증에 필요한 모든 정보는 토큰 자체에 포함하기 때문에 별도의 인증 저장소가 필요 없다.
  - 트래픽 대한 부담이 낮다.
- 단점
  - 토큰 자체에 모든 정보를 담고 있으므로 보안 이슈
    - 이 토큰을 통제하는 것이 핵심이며 구현이 다소 복잡하다는 점..?
  - 토큰 길이: 토큰의 페이로드(Payload)에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있다.
  - Stateless: JWT는 상태를 저장하지 않기 때문에 한번 만들어지면 제어가 불가능하다. 즉, 토큰을 임의로 삭제하는 것이 불가능하므로 토큰 만료 시간을 꼭 넣어주어야 하다.
  - 토큰은 클라이언트 측에서 관리해야 하기 때문에, 토큰을 저장해한다.

출처: https://velog.io/@dnjscksdn98/JWT-JSON-Web-Token-%EC%86%8C%EA%B0%9C-%EB%B0%8F-%EA%B5%AC%EC%A1%B0



## 인증 방식으로 JWT를 사용하는 이유

### 인증 방식으로 토큰 선택 이유

세션 대신 토큰을 사용하려는 이유는 확장성 때문이다. 만약 여러 서버가 돌아가는 상황이라면, 각 서버마다 세션 저장소를 두거나, 공통 세션 저장소를 만들어야하는데, 이 또한 비용이다. 반면에 토큰은 stateless 하기 때문에 확장에 용이하다.

다만, 토큰은 한 번 발급되면 강제로 만료시킬 수 없다는 단점이 있다. 따라서 만료 시간이 짧은 access token과 만료 시간이 긴 refresh token을 나눠서 사용하는 것이다.

토큰은 실제로 로그인을 유지하고 있는 것이 아니라 로그인이 유지된 것 처럼 행동한다.(클라이언트가 access token을 저장해두고, 요청 때 마다 보내는 방식) 따라서 만약 access token이 만료된 것이 아니라면, 로그아웃을 했더라도 해당 access token만 가지고 있다면, 로그인 된 상태처럼 행동할 수 있다고 한다.

출처: https://velog.io/@max9106/OAuth



## JWT 구조

- 헤더 (Header)

  - type: 토큰의 타입을 지정한다 (jwt)

  - alg: 해싱 알고리즘을 지정한다. 보통 'HMAC SHA256' 혹은 'RSA'가 사용된다. 이 알고리즘은 토큰을 검증할 때 signature부분에서 사용된다.

  - 예시

    - ```
      {
        "typ": "JWT",
        "alg": "HS256"
      }
      ```

- 정보 (Payload)

  - 토큰에 담을 정보가 들어있다. 여기서 담는 정보의 한 '조각'을 클레임(claim)이라고 부른다.

  - 클레임은 name / value 한 쌍으로 이뤄져있다. 토큰에는 여러 개의 클레임을 넣을 수 있다.

  - 클레임의 종류

    - registered: 등록된 클레임

      - 서비스에서 필요한 정보들이 아닌 토큰에 대한 정보를 담기 위한 클레임이다.
      - 등록된 클레임의 사용은 선택적(optional)이며, 포함된 클레임은 아래와 같다.
        - `iss`: 토큰 발급자 (issuer)
        - `sub`: 토큰 제목 (subject)
        - `aud`: 토큰 대상자 (audience)
        - `exp`: 토큰의 만료시간 (expiraton), 시간은 NumericDate 형식으로 되어있어야 하며 (예: 1480849147370) 언제나 현재 시간보다 이후로 설정되어있어야 한다.
        - `nbf`: Not Before 를 의미하며, 토큰의 활성 날짜와 비슷한 개념이다. 여기에도 NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않는다.
        - `iat`: 토큰이 발급된 시간 (issued at), 이 값을 사용하여 토큰의 `age` 가 얼마나 되었는지 판단할 수 있다.
        - `jti`: JWT의 고유 식별자로서, 주로 중복적인 처리를 방지하기 위하여 사용됩니다. 일회용 토큰에 사용하면 유용하다. 

    - public: 공개 클레임

      - 공개 클레임은 충돌 방지(collision-resistant)를 위해 name을 uri형식으로 짓는다.

      - 예시

        - ```
          {
              "https://velopert.com/jwt_claims/is_admin": true
          }
          ```

    - private: 비공개 클레임

      - 공개 클레임과는 달리 충돌 가능성이 있으므로 주의해야 한다.

    - 예시 Payload

      - ```
        {
            "iss": "velopert.com",
            "exp": "1485270000000",
            "https://velopert.com/jwt_claims/is_admin": true,
            "userId": "11028373727102",
            "username": "velopert"
        }
        ```

- Signature

  - 서명(Signature)은 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드다.

출처: https://velopert.com/2389



# JWT 토큰의 보안 전략

Refresh Token 도입 전략과 Sliding Session 전략, 그리고 이를 모두 활용한 전략 모두를 소개한다.

아래에도 적어놓겠지만, 내용 출처는 바로 이 곳 -> https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html이다.



## JWT Access Token

사용자가 로그인을 할 때 클라이언트에게 AccessToken을 발급한다. 서버는 AccessToken을 데이터베이스나 파일등에 저장 할 필요 없이 메모리상에서 미리 정의 된 비밀키를 이용해 비교하는 것 만으로 인증을 처리하기 때문에 추가적인 I/O 작업이 필요가 없다. 반면에 그런 이유로 서버는 특정 사용자의 접속을 강제로 만료시키기 어려워진다. 따라서 이를 위해 클라이언트는 스스로의 저장 공간에서 토큰을 삭제하는 방법을 사용해 사용자의 접근을 막는다.

### 짧은 만료 시간(30분 내외)을 설정할 경우 

#### 장점

- 기기나 AccessToken이 탈취되더라도 빠르게 만료된다.

#### 단점

- 사용자는 자주 로그인을 해야 한다. 한 사용자가 오랫동안 상주하는 서비스라면 서비스를 이용하는 도중에 갑자기 인증이 만료되어 로그인창이 뜨는 경우를 볼 수 있다.

### 긴 만료 시간(2주에서 한달)을 설정할 경우

#### 장점

- 사용자가 로그인을 자주 할 필요가 없다.

#### 단점

- 기기나 AccessToken이 탈취되면 오랫동안 제약 없이 사용이 가능하므로 보안에 취약하다.



출처: https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html



이처럼 사용자의 로그인 편의성과 보안성 사이에서 Trade-off가 존재한다. 



## Sliding Sessions 전략 도입

보안성과 편의성 모두를 잡기 위해 고안된 것이 Sliding Sessions 전략입니다. 이 전략은 세션을 지속적으로 이용하는 유저에게 자동으로 만료 기한을 늘려주는 방법이다.

구현 방법은 다양하다. 주로 유효한 AccessToken을 가진 클라이언트의 요청에 대해 서버가 새로운 AccessToken을 발급해주는 방법을 사용한다. 매 요청마다 새로운 토큰을 내려주는 것도 가능하지만, 클라이언트가 장시간 인증이 요구되는 작업(ex. 글 작성)을 하다가 인증이 만료되어 발생하는 참담한 경우를 막기 위해 글 작성을 시작할 때 발급해준다거나, 쇼핑몰에서 장바구니에 아이템을 담는 경우에 발급해주는 등의 전략을 사용하는 것도 괜찮은 방법이다. 또 클라이언트가 토큰의 iat(토큰 발급 시간)속성을 참조해서 갱신 요청을 하는 방법도 있다.

이 방법을 활용하면 AccessToken만을 이용해 인증을 처리할 때 있었던 단점을 보완할 수 있다.

#### 장점

- 사용자가 로그인을 자주 할 필요가 없다.
- 글을 작성하거나 결제를 하는 등의 세션 유지가 필요한 순간에 세션이 만료되는 문제를 방지 할 수 있다.

#### 단점

- 접속이 주로 단발성으로 이루어지는 서비스의 경우 Sliding Sessions 전략의 효과가 크지 않다.
- 긴 만료 시간을 갖는 AccessToken을 사용하는 경우 로그인을 전혀 하지 않아도 되는 경우가 발생한다.



출처: https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html



## Refresh Token 도입

사용자가 로그인을 할 때에 AccessToken과 함께 그에 비해 긴 만료 시간을 갖는 RefreshToken을 클라이언트에 함께 발급하는 방법이다. 주로 AccessToken은 30분 내외, RefreshToken은 2주에서 한달 정도의 만료 기간을 부여한다.

클라이언트는 AccessToken이 만료되었다는 오류를 받으면 따로 저장해두었던 RefreshToken을 이용하여 AccessToken의 재발급을 요청한다. 서버는 유효한 RefreshToken으로 요청이 들어오면 새로운 AccessToken을 발급하고, 만료된 RefreshToken으로 요청이 들어오면 오류를 반환해, 사용자에게 로그인을 요구한다.

AccessToken은 서버에 따로 저장해 둘 필요가 없지만, RefreshToken의 경우 서버의 stroage에 따로 저장해서 이후 검증에 활용해야 한다. 그러므로 RefreshToken을 이용한다는 것은 추가적인 I/O 작업이 필요하다는 의미이며, 이는 I/O 작업이 필요없는 빠른 인증 처리를 장점으로 내세우는 JWT의 스펙에 포함되지 않는 부가적인 방식이다.

RefreshToken은 탈취되어서는 곤란하므로 클라이언트는 보안이 유지되는 공간에 이를 저장해두어야 한다. 또한 RefreshToken은 서버에서 따로 저장을 하고 있기 때문에 강제로 토큰을 만료시키는 것이 가능해진다.

#### 장점

- 짧은 만료 기간을 사용 할 수 있기 때문에 AccessToken이 탈취되더라도 제한된 기간만 접근이 가능하다.
- 사용자가 로그인을 자주 할 필요가 없다.
- RefreshToken에 대한 만료를 강제로 설정 할 수 있다.

#### 단점

- 클라이언트는 AccessToken의 만료에 대한 연장 요청을 구현해야 한다.
- 인증 만료 기간의 자동 연장이 불가능하다.
- 서버에 별도의 storage를 만들어야 한다.

출처: https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html



## Sliding Sessions 전략과 Refresh Token을 모두 활용한다면

AccessToken의 Sliding Sessions 전략이 AccessToken 자체의 만료 기간을 늘려주었다면, 이 전략은 RefreshToken의 만료 기간을 늘려준다.

RefreshToken의 만료 기간이 늘어나기 때문에 AccessToken + Sliding Sessions 전략처럼 빈번하게 만료 기간 연장을 해줄 필요가 없고, 사용자의 유휴 허용 기간을 RefreshToken 기간에 근접하게 늘려준다.

반면 사용자가 접속을 뜸하게 하는 경우에도 RefreshToken의 만료 기간의 늘어나기 때문에, 핸드폰이 탈취되는 등의 경우에 지속적인 이용이 가능 할 수 있다는 단점이 있다. 이를 막는 방법으로 인증이 확실히 요구되는 경우 비밀번호를 한번 더 묻는다거나, 비밀번호 변경 등의 이벤트가 발생 할 때 강제로 RefreshToken을 만료시키는 처리를 해주는 것이 좋다.

#### 장점

- RefreshToken의 만료 기간에 대한 제약을 받지 않는다.
- 글을 작성하거나 결제를 하는 등의 세션 유지가 필요한 순간에 세션이 만료되는 문제를 방지 할 수 있다.

#### 단점

- 서버에서 강제로 RefreshToken을 만료하지 않는 한 지속적으로 사용이 가능하다.
- 인증이 추가로 요구되는 경우에 대한 보안 강화가 필요하다.



출처: https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html



이 부분은 명확히 이해가 되지 않아 좀더 조사를 진행하였고, 더 자세하게 설명한 글을 찾아서 가져와 보았다.



### 토큰 발행 전략 / Sliding Sessions

슬라이딩 세션은 일정 기간 이후에 만료가 되어지는 세션들을 의미한다. 이러한 슬라이딩 세션은 access token 과 refresh token 들을 사용하면 쉽게 구현될 수 있다. 유저가 로그인을 통하여 새로운 엑세스 토큰이 발행되고, 그 이후에 유저의 엑세스 토큰이 만료가 된다면, 그 세션은 비활성화가 되고, 새로운 토큰이 필요해진다. 이때, 이 토큰이 refresh token 을 통하거나 또는 새로운 인증 과정을 거쳐서 access token 을 얻거나 하는 방식은 개발 팀의 요구사항에 따라 정의될 수 있다. 이처럼 어떤 세션이 무조건 재 로그인을 통해서 access token 을 받는 방식이 아니라, access token 이 만료가 되더라도 로그인이 아닌 방식을 통해서 새로운 access token 을 다시 발행을 받으면서 만료 시간을 아래 그림처럼 계속 늘려나갈 수 있는 방식을 슬라이딩 세션, 문자 그대로 움직이는 세션이다.

출처: https://www.dazhuanlan.com/bility/topics/1685835



<img src="https://user-images.githubusercontent.com/71204049/143216622-aa247c25-0c09-4bba-8d10-d8f889b91136.png" width="700" />



### 구현 방법 - Access Token, Refresh Token With Sliding Session

이는 access token 이 만료가 되어 refresh token 으로 access token 을 새로 발급 받을 때, refresh token 은 한번만 사용되고 즉시 폐기 처리가 되고, 새로운 refresh token 을 함께 발행해주는 방법이다. 이 방법을 사용하게 되면, 슬라이딩 세션을 지키면서 만약 유저가 refresh token 의 만료 기간내에 접속을 하지 않을 경우에는 재 로그인을 하게 함으로써 보안성은 지키고, 자주 사용하는 유저의 경우에는 토큰이 만료될 때마다 새로운 access token 과 refresh token 을 함께 받아오기 때문에 로그아웃이 되는 문제를 보완해줘서 유저의 편의성도 지킬 수 있다. 다만, 만약 이 refresh token 이 탈취가 되었다면, 계속적으로 새로운 토큰을 받아 갈 수 있기 때문에 보안 문제가 발생할 수 있다. 이러한 부분은 ‘비밀번호 변경’ 등을 통해 refresh token 을 강제로 만료시켜 버리는 방법을 통해 해결할 수도 있다.

출처: https://www.dazhuanlan.com/bility/topics/1685835



## 전략들에 대한 결론

일반적인 웹 서비스처럼 cookie등을 이용해 세션 관리를 하는 방식을 사용할 수 없는 stateless한 REST API등은 토큰 방식의 보안을 이용할 수 밖에 없다. stateless하기 때문에 매 요청에 대한 인증을 거쳐야 하는데, 이는 데이터베이스 등으로부터 토큰을 얻어오는 추가적인 I/O 작업이 불가피하고 이는 성능의 하락으로 이어진다. 이를 **해결해주기 위한 솔루션이 바로 JWT**이다.

JWT는 이런 장점과 함께 위에서 살펴봤듯이 여러가지 문제점들이 존재한다. 

- 토큰의 탈취에 대한 취약성
- 서버의 클라이언트 제어 불가
- 빈번한 로그인 요청 등의 문제

이에 대한 해결 방법은 RefreshToken이나 Sliding Sessions 등의 전략을 도입하는 것이다. 하지만 이러한 전략들 역시 추가적인 IO 작업을 위한 성능 감소나, 편의를 위해 보안이 취약해지는 상황등이 발생할 가능성이 있다.

서비스가 결제가 필요한 보안에 민감한 컨텐츠를 다루고 있다면 비밀번호 한번 더 입력하는 것이 크게 문제가 되지 않는다. 반면, 게시물에 글을 작성할때마다 비밀번호를 입력해야 한다면 사용자들은 매우 귀찮아 할 것이다. 결국 모든 것을 얻을 수는 없다. 서비스마다 가진 고유한 특성을 고려해 보안 수준을 높일지, 사용자 편의성을 높일지를 결정해야 한다.

출처: https://blog.ull.im/engineering/2019/02/07/jwt-strategy.html





## OAuth와 JWT 함께 활용한 설계 예시

<img src="https://user-images.githubusercontent.com/71204049/143212053-7aaa9777-7874-4ab5-9325-2ce7da9a496a.png" width="700" />

출처: https://velog.io/@max9106/OAuth

### 프론트엔드 역할

- OAuth Authorization Server로  로그인 요청 후, Authorization code 발급 받아, 백엔드에 전달
- 백엔드에서 응답 받은 access token, refresh token 저장해둔다.
- 권한이 필요한 요청마다 Authorization 헤더에 access token 같이 보내주기
- access token이 만료되었다면, refresh token 보내서 갱신하기(프론트에서 요청 날릴 때 access token이 만료됨을 미리 판별하여 갱신 요청을 보낼 수 있음)
- refresh token 만료 기간이 7일 이내면, refresh token 재발급 요청

### 백엔드 역할

- Authorization code로 github OAuth 서버에 토큰 요청
- (로그인 할 때 이외에 OAuth 서버와 통신이 필요한 경우 발급 받은 토큰 저장해야 할듯)
- Access token으로 이름, 이메일, 프로필 URL 정보 요청
- db에 존재하지 않는 유저라면, 새로 등록. db에 존재하는 유저라면 정보 업데이트
- 유저의 primary key 값으로 JWT 토큰(access token & refresh token) 생성. 일반적으로 access token은 한 시간, refresh token은 2주로 생성(본인 애플리케이션에 맞게 변경하여 사용)
- refresh token은 DB나 Redis에 저장
- 유저 정보, access token, refresh token 프론트로 전달
- access token 만료시 refresh token 검증 후, 재발급

출처: https://velog.io/@max9106/OAuth





## 추가적으로 참고한 글 목록

https://sun-22.tistory.com/44

https://tristan91.tistory.com/499

https://velog.io/@tmdgh0221/Spring-Security-%EC%99%80-OAuth-2.0-%EC%99%80-JWT-%EC%9D%98-%EC%BD%9C%EB%9D%BC%EB%B3%B4



