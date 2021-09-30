> 김영한님의 [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/) 강의를 듣고 정리하였습니다. 
>
> 또한, [망나니개발자님의 블로그](https://mangkyu.tistory.com/91)를 참조하였습니다.




## 인터넷 네트워크

클라이언트와 서버는 **인터넷**을 통해 데이터를 주고 받는다.

<img src="https://user-images.githubusercontent.com/71204049/135503901-41dbcbbf-7ed7-411e-aba0-5a0decea0bbe.png" width="500" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))





## 인터넷 프로토콜(IP)이란?



<img src="https://user-images.githubusercontent.com/71204049/135504549-3c554a9d-3e57-4071-83cb-bcce883cea86.png" alt="img" width="710" />

(사진 출처: [벨로그](https://velog.io/@mark91/%EC%9D%B8%ED%84%B0%EB%84%B7-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC))



복잡한 인터넷 망에서 Client와 Server간에 통신을 하려면 최소한의 규칙이 필요한데, 이것이 바로 **IP**이다.





## 인터넷 프로토콜(IP) 역할

- 지정한 IP 주소(IP Address)에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 데이터 전달





## IP 패킷의 구성

출발지 IP, 목적지 IP, 데이터 및 기타 정보를 포함한다.

<img src="https://user-images.githubusercontent.com/71204049/135504623-be3b3cc7-16eb-4ff9-848e-3c5d50445ae2.png" alt="img" width="500" />

(사진 출처: [네이버 블로그](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=jyj9372&logNo=50170030307))





## IP 프로토콜의 한계

- 비연결성

  - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송

- 비신뢰성

  - 목적지까지 패킷의 정확한 전송을 보장하지 않음

    -> 중간에 패킷이 사라지면?

    -> 패킷이 순서대로 안오면?

- 프로그램 구분

  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?





## OSI 7계층 및 TCP/IP 4계층 구조

<img src="https://user-images.githubusercontent.com/71204049/135504135-0d3e3f21-d362-4a37-80c3-40b61056e356.png" width="500" />

(사진 출처: [티스토리](https://parodev.tistory.com/28))



## TCP(Transmission Control Protocol)

TCP는 전송 계층의 대표적인 연결지항 프로토콜이다.

TCP 패킷은 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보 등을 포함한다.



## TCP/IP 패킷 정보

<img src="https://user-images.githubusercontent.com/71204049/135504214-4bb960d0-1d21-4a0c-aa36-836e588cb6eb.png" width="500" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))



## TCP 특징

- 연결 지향 프로토콜
- 가상 회선 방식
-  TCP 3 way handshake (연결 설정) 및 4 way handshake (연결 해제)
- 흐름 제어 및 혼잡 제어
- 데이터 전달 보증
- 전송 순서 보장

- 높은 신뢰성 보장
- UDP보다 느린 속도



## TCP 3 way handshake 

정확한 전송을 보장하기 위해, 사전에 통신하는 장치 간의 논리적 연결을 확인하고 세션을 수립하는 과정

<img src="https://user-images.githubusercontent.com/71204049/135504285-e907a373-e420-4fb6-9efb-3247a33bfa36.png" width="500" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))



## UDP (User Datagram Protocol)

- 하얀 도화지에 비유할 수 있다. 기능이 거의 없다.
- 비연결형 서비스
- 데이터그램 방식
- 데이터 전달 보증 X
- 순서 보장 X
- 빠름
- IP와 유사 + PORT(프로그램 구분) + 체크섬(메시지에 대한 검증)
- 애플리케이션에서 추가 작업 필요



## TCP vs UDP

TCP는 연결형 서비스로 3-way handshaking 과정을 통해 연결을 설정한다. 그렇기 때문에 높은 신뢰성을 보장하지만 속도가 비교적 느리다는 단점이 있다. 

UDP는 비연결형 서비스로 3-way handshaking을 사용하지 않기 때문에 신뢰성이 떨어지는 단점이 있다. 하지만 수신 여부를 확인하지 않기 때문에 속도가 빠르다. 애플리케이션 레벨에서 기능을 확장하는 등 최적화가 가능하다.

TCP는 신뢰성이 중요한 파일 교환과 같은 경우에 쓰이고 UDP는 실시간성이 중요한 스트리밍에 자주 사용된다.



## PORT

같은 IP 내에서 프로세스(통신할 어플리케이션) 구분한다.

<img src="https://user-images.githubusercontent.com/71204049/135504340-7d245d51-5d18-43f1-a0d7-c01efecbf5e7.png" width="500" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))



IP가 아파트라면 PORT는 몇 동, 몇 호인지 나타낸다.

- 0 ~ 65535: 할당 가능 
- 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋음
  - FTP - 20, 21
  - TELNET - 23
  - HTTP - 80
  - HTTPS - 443



## DNS (Domain Name System)

IP는 기억하기 어렵다.

IP는 변경될 수 있다.

DNS는 도메인 명을 IP 주소로 변환한다.

<img src="https://user-images.githubusercontent.com/71204049/135504405-2f4762eb-fe54-4717-ae3c-ad8e1209e3f1.png" width="580" />

(사진 출처: [인프런 강의](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/))
