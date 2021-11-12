> 이석복 교수님의 [컴퓨터네트워크](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>



## Client-Server Architecture

- server
  - 바뀌지 않는 고정된 IP 주소를 가져야 함
- client
  - IP 주소를 가지고 있되, 고정되지 않아도 됨



## Sockets

- 소켓은 프로세스가 네트워크를 통해 데이터를 보내거나 받기 위한 실제적인 창구 역할을 한다.
- 소켓의 주소(인덱싱) 역할은 IP와 Port가 담당한다.
  - IP: 인터넷 상에 존재하는 컴퓨터의 위치
  - Port: 하나의 컴퓨터에 존재하는 여러 프로세스 중 하나를 특정



## Port를 통일하는 이유

웹 브라우저를 이용해 구글, 네이버 등 웹페이지를 접속할 때 우리는 일반적으로 www.google.com, www.naver.com 과 같은 url을 입력한다. 이는 DNS를 거쳐 IP로 변환되고 생략된 port는 기본값이 80이다.

모든 웹 서비스의 port가 제각기 다르다면 각각의 웹페이지에 접속하기 위해 우리는 매번 port를 입력해야하고 이는 번거로운 일이다. 따라서 http 기본 port를 80으로 통일한다. 



## 앱이 네트워크에 기대하는 4가지

1. Data Integrity

   - 중간에 유실되는 문제 없이 정확하게 데이터가 전송되는 것

2. Timing

   - 데이터가 전달되는 속도

   - low delay, 빠른 전송 속도

3. Throughput

   - 단위 시간당 디지털 데이터 전송으로 처리하는 양

   - 빠른 처리량

4. Security

   - 전송되는 과정에서의 보안



**Transport Layer에서는 1번만을 보장한다 (TCP 한정) . Security는 Application Layer에서 구현한다.**





## HTTP

- Hypter Text Transfer Protocol: 하이퍼텍스트를 전송하는 프로토콜
- Application Layer 프로토콜이다.
  - 특히, Transport Layer의 TCP를 사용한다.
- 클라이언트-서버 모델
  - 클라이언트의 Http Request
  - 서버의 Http Response
- Stateless
  - Client의 상태를 저장하지 않는다.



## Persistent vs Non-persistent

- Persistent 방식
  - 추가적으로 요청할 오브젝트가 있을 수 있기 때문에 소켓 연결을 끊지 않고, 바로 다시 요청을 할 수 있다.
  - 병렬 요청 (파이프라인)
- Non-Persistent 방식
  - 하나의 Request에 대한 Response 후 접속(Connection)을 끊는다.
  - Connection: close를 하지 않아도 소켓 연결이 알아서 끊긴다.





