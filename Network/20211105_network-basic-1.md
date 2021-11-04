> 이석복 교수님의 [컴퓨터네트워크](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>



## 네트워크 구조 살펴보기

- Network Edge
  - Applications, hosts, laptop, desktop, servers 등
- Network Core
  - Routers
    - 라우터들이 연결되어있어 데이터들을 전송한다.
  - Network of Networks
- Access Networks, Physical Media
  - Communication links
    - 네트워크 구성요소들을 이어준다.



## The Network Edge

- end systems (hosts):
  - 어플리케이션 프로그램을 실행한다
    - 예) 웹, 이메일 등
- 클라이언트 서버 모델
  - 클라이언트(호스트)는 항상 켜져있는 서버로부터 서비스를 요청하고 제공받는다.
    - 예) 웹 브라우저/서버, 이메일 클라이언트/서버
- peer to peer model (P2P)
  - minimal use of dedicated servers
    - 예) Skype, BitTorrent, KaZaA



## Network Edge: Connection-oriented Service(연결 지향형 서비스)

- TCP (Transmission Control Protocol)

  - 연결 지향형 서비스를 제공하는 통신 방법
  - 특징
    - 연결의 설정(3-way handshaking)과 해제(4-way handshaking)
    - Reliable
      - 신뢰성있는 데이터를 전송한다.
      - Sequence Number, Ack Number를 통한 신뢰성 보장
    - in-order, byte-stream service
      - 데이터의 전송 순서를 보장한다.
      - 바이트 스트림 서비스를 제공한다.
    - flow control (흐름 제어)
      - 송신 측과 수신 측의 데이터 처리 속도 차이를 해결
      - 수신 측이 송신 측보다 빠르면 문제없지만, 송신 측의 속도가 빠를 경우 문제가 생긴다.
      - 수신 측에서 제한된 저장 용량을 초과한 이후에 도착하는 데이터는 손실 될 수 있으며 만약 손실된다면 불필요하게 응답과 데이터 전송이 송/수신 측 간에 빈번이 발생한다.
      - 따라서 Receiver의 처리 속도에 맞추어서 Sender의 전송 속도를 조절한다.
    - congestion control (혼잡 제어)
      - 네트워크 내에 패킷의 수가 과도하게 증가하는 현상을 혼잡(Congestion)이라한다.
      - 송신측의 데이터는 지역망이나 인터넷으로 연결된 대형 네트워크를 통해 전달된다. 만약 한 라우터에 데이터가 몰릴 경우, 자신에게 온 데이터를 모두 처리 할 수 없게 된다. 
      - 이런 경우 호스트들은 또 다시 재전송을 하게되고 결국 혼잡만 가중시켜 오버플로우나 데이터 손실이 발생한다.
      - 이러한 혼잡 현상을 방지하기 위해 송신 측에서 보내는 데이터의 전송 속도를 줄인다.
      - 흐름 제어가 송신 측과 수신 측 사이의 전송 속도를 다루는 데 반해 혼잡 제어는 호스트와 라우터를 포함한 보다 넓은 관점에서의 전송 문제를 다룬다.
    - 신뢰성을 보장하는 대신 비교적 느리다.
    - 비싸다.
      - 컴퓨팅 리소스와 네트워크 리소스를 더 많이 소모한다.

  

  (내용 출처: [티스토리](https://jwprogramming.tistory.com/36#))





## Network Edge: Connectionless Service(비연결형 서비스)

- UDP (User Datagram Protocol)
  - 비연결형 서비스를 제공하는 통신 방법
  - 특징
    - Connectionless
      - 비연결형
    - Unreliable data transfer
      - 데이터의 신뢰성을 보장하지 않음
      - 데이터가 유실될 수 있다.
    - No flow control
    - No congestion control
    - 신뢰성을 보장하지 않는 대신 비교적 빠르다.
      - 왜?
        - TCP와 달리 연결의 설정/해제가 필요없고, 데이터의 신뢰성을 보장할 필요없고, 흐름 제어 및 혼잡 제어도 하지 않으므로 송신자는 전송 속도를 원하는 대로 높일 수 있음 (대신 데이터가 유실될 수 있다는 것. 데이터가 잘 도착한다는 보장이 없다.)
      - 언제 쓸까?
        - Realtime Voice (음성 전화)
          - 오디오 패킷이 몇 개 유실되도 사람들이 크게 감지하지 못함. 괜찮다.
    - 싸다.
      - 컴퓨팅 리소스와 네트워크 리소스를 적게 소모한다.



## 프로토콜이란?

-  컴퓨터나 원거리 통신 장비 사이에서 메시지(데이터)를 주고 받기 위한 양식과 규칙의 체계이다.





## The Network Core

- 네트워크 코어에는 라우터들이 존재해서 이들이 상호작용하여 데이터를 목적지까지 데려다 준다.
- 라우터는 어떠한 방식으로 데이터를 전달할까?
  - 메시지의 전달 방식
    - circuit switching
      - 유선 전화망에서 사용
      - 출발지에서 목적지까지 가는 경로를 미리 예약을 해두고 특정 사용자들이 사용할 수 있도록 만들어 놓는 것이다.
      - 데이터가 호스트에서 목적지로 가는 경로가 단 하나, 즉 유일한 경로를 통해 데이터를 전송한다.
    - packet switching
      - 송신할 데이터를 packet이라는 단위로 쪼개서 전송한다.
      - 인터넷에서 사용
      - 유저가 보내는 패킷들을 그때그때 올바른 방향으로 전송(forwarding)하는 것이다.
      - 모든 링크를 사용할 수 있다. 전송된 패킷들은 목적지에만 연결되어 있다면 네트워크 상의 어떤 링크든지 타고 갈 수 있다.
      - 이러한 과정에서 패킷은 다음 라우터로 이동하기 위해 큐에서 대기(queueing)하는데 이 때 수용할 수 있는 큐의 범위를 초과하게 되면 손실(loss), 즉 패킷 유실이 발생하게 된다.



## 패킷 지연 4가지 유형

- Nodal processing delay (노드 처리 지연)
  - 라우터 자체 작업
  - 데이터 패킷 헤더의 처리
  - 비트 데이터 오류 체크
  - 네트워크 패킷을 라우터로 전송할 때 라우터에서 패킷 헤더를 검사하여 어느 출력 링크로 전송할지 결정한다.
- Queuing delay (큐잉 지연)
  - 여기서 큐(Queue)란?
    - 데이터 패킷을 라우터로 전송하는 속도가 빠르면 라우터에서 제 때 처리하지 못해 해당 패킷을 일시적으로 완충 구역인 큐에 머물러 대기 후 전송하게 된다. 이 때의 지연 시간을 Queueing Delay라고 한다.
  - 패킷이 큐에서 출력 링크로 전송되기를 기다리는 시간
  - 라우터 혼잡 수준(congestion level)에 좌우 된다. 즉, 이미 큐에 저장된 패킷들의 수에 의해 결정된다.
- Transmission delay (전송 지연)
  - 패킷의 모든 비트들을 링크로 밀어내는(전송)데 필요한 시간
  - 네트워크 장비의 데이터 전송 속도로 결정되며, 서버-클라이이언트 간의 거리와는 무관하다.
- Propagation delay (전파 지연)
  - 출력 링크에서 다음 라우터까지 전파하는데 필요한 시간
  - 전파 속도는 링크의 물리 매채(광섬유, 고임쌍선 등)에 좌우
  - 즉, 신호의 전송거리와 전송 매개체로 결정된다. 

(내용 출처: [티스토리1](https://corona-world.tistory.com/47), [티스토리2](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=three_letter&logNo=220505813304))
