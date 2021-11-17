> 이석복 교수님의 [컴퓨터네트워크](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>



## Application Layer

- TCP/IP 5계층 모델에서 가장 상위 Layer를 담당한다.

- Transport/Network/Link/Physical Layer는 모두 운영체제에 구현

- 방식 2가지

  - Client-Server

    - Client: 서비스를 제공받는 호스트
    - Server: 서비스를 제공하는 호스트
    - **중앙 집중된 서버가 존재**
      - 클라이언트 수가 증가하면 네트워크 부하가 발생
    - 중앙 집중적으로 관리되므로 접근 허가/제한에 용이함
    - 서버 구축 비용이 많이 든다.
    - 서버가 다운될 경우 연결된 클라이언트들은 서비스를 모두 서비스를 제공받을 수 없게 된다.

  - P2P(Peer-to-Peer)

    - 컴퓨터 간의 양방향 파일 전송 시스템
    - **중앙 서버 없이 각각의 컴퓨터가 서버와 클라이언트가 된다.**
      - **모든 단말이 동일하고 특별한 기능과 역할을 가진 단말이 존재하지 않는다.**
      - 사용자 수가 방대해져도 특정 단말에 부하가 집중되지 않는다 -> 확장성
    - 설치와 관리가 간편하고 고가의 서버 등을 구입할 필요가 없다.
      - 구축에 많은 비용이 소모되지 않음
    - 데이터가 여러 컴퓨터에 흩어져 있어 백업 작업이 복잡하다.
    - 새로운 기능 추가나 업데이트 관리가 어렵다.

    

## Socket

- 컴퓨터 네트워크를 경유하는 프로세스 간 통신의 종착점이다(endpoint).

- 구성 요소 5가지

  - 인터넷 프로토콜(TCP, UDP)
  - 로컬 IP 주소
  - 로컬 port
  - 원격 IP 주소
  - 원격 port

- 소켓은 크게 두 개 타입으로 분류할 수 있다.

  - TCP 프로토콜을 사용하는 경우
  - UDP 프로토콜을 사용하는 경우

- 어플리케이션 계층(Application Layer)에 존재하는 네트워크 응용 프로그램들은 데이터를 송수신 하기 위해 소켓을 거쳐 전송 계층(Transport Layer)의 통신 망으로 전달한다.

  - 즉, 운영체제의 핵심인 커널에 어플리케이션에서 생성되는 메시지를 전달해주는 과정에서 socket이 활용된다.

  - application layer와 transport layer 사이에 위치

    <img src="https://user-images.githubusercontent.com/71204049/142155249-d8498a15-5f50-459c-8e7d-42043794b78f.png" width="600" />

    (사진 출처: [티스토리](https://ddongwon.tistory.com/71))



## Socket 프로그래밍

- Socket 연결은 TCP/IP 프로토콜을 기반으로 맺어진 네트워크 연결 방식
- 이러한 Socket 연결 방식으로 프로그래밍 하는 것이 소켓 프로그래밍
- Server와 Client가 특정 Port를 통해 연결을 유지하며 **실시간으로 양방향 통신**을 하는 방식
- HTTP 프로그래밍과의 차이
  - Socket 프로그래밍은 Server 역시 Client로 요청을 보낼 수 있으며, 계속 연결을 유지하는 연결지향형 방식이기 때문에 실시간 통신이 필요한 경우에 자주 사용
  - 실시간 양방향 통신 vs 요청이 있을 때만 클라이언트에서 서버로의 일회성 단방향 통신
- 실시간 채팅이나 동영상 스트리밍 서비스, 온라인 게임 등에 사용
  - HTTP 프로그래밍을 사용한다면?
    - 실시간 채팅의 경우 HTTP 프로그래밍으로 구현 자체가 불가능. 송신은 가능하지만 수신자가 실시간으로 연결되어 있지 않기 때문
    - 동영상 스트리밍 서비스의 경우 동영상이 종료되는 순간까지 계속해서 HTTP 요청을 보내야 하기 때문에 서버에 많은 부하가 발생
  - Socket을 사용하는 것이 적합



## HTTP 프로그래밍

- 기본적으로 소켓 연결 위에서 맺어지는 어플리케이션 계층의 연결 방식
  - http도 소켓 위에서 동작한다.
- Client의 요청(Request)이 있을 때만 Server가 응답(Response)하여 해당 정보를 전송하고 곧바로 연결을 종료하는 방식
- 실시간 연결이 아닌, 필요한 경우에만 Server로 접근하는 콘텐츠 위주의 데이터를 사용할 때 용이하다.
- 필요한 경우에만 Server로 정보를 요청하는 경우가 많다. Web Server에서 Http 프로그래밍 방식을 주로 사용하며 비용 및 유지보수 등 대부분의 방면에서 좋다. 





## 소켓 통신의 흐름

<img src="https://user-images.githubusercontent.com/71204049/142147764-8d6537ba-aefe-4597-a899-8b74805e550b.png" width="600" />

(사진 출처: [티스토리](https://recipes4dev.tistory.com/153))



### socket()

```c
int socket(int domain, int type, int protocol);
```

- 소켓을 생성한다.

- 소켓 역시 파일로 이루어져있기 때문에 파일 디스크립터를 반환한다.

- 소켓을 여는데 실패했다면 -1을 반환한다.

- 3가지 인자

  - domain: 프로토콜 패밀리 지정()

    - **- PF_INET : 인터넷 프로토콜** (TCP/IP를 사용하기 위해 기본적으로 인터넷 프로토콜 지정)

      \- PF_INET6 : IENT IPv6 프로토콜

      \- PF_UNIX : 유닉스 방식 프로토콜

      \- PF_NS : 제록스 네트워크 시스템의 프로토콜

      \- PF_PACKET : 리눅스에서 패킷 캡쳐를 위해 사용

  - type: 프로토콜에 따라 3가지 방식

    - TCP
    - UDP
    - raw (TCP나 UDP를 거치지 않고 바로 IP 계층 사용 시)

  - protocol: 소켓에서 사용할 프로토콜

    - **protocol : 소켓에서 사용할 프로토콜**

      \- IPPROTO_TCP : TCP 방식

      \- IPPROTO_UDP : UDP 방식

      \- 0 : type에서 미리 정해진 경우 써도 됨



### bind()

```c
int bind(int sockfd, struct sockaddr *addr, socklen_t addrlen);
```

- 소켓에 주소를 할당한다.
- 3가지 인자
  - sockfd: socket() 함수를 통해 배정받은 파일 디스크립터 번호
  - *addr: IP주소와 port번호를 담은 구조체
  - addrlen: addr 변수의 길이



### listen()

```c
int listen(int sock, int backlog);
```

- 연결 요청을 대기한다.
- 2가지 인자
  - sock: 소켓 디스크립터 번호
  - backlog: 연결 요청을 대기하는 큐의 크기



### connect()

```c
int connect(int fd, struct sockaddr *remote_host, socklen_t addr_length)
```

- 서버 소켓에 연결을 요청하는 함수
- 3가지 인자
  - fd: 소켓 디스크립터 번호
  - sockaddr: 원격 호스트의 주소 정보를 담음(IP주소, Port번호)
  - addr_length: sockaddr 변수의 길이



### accept()

```c
int accept(int sock, struct sockaddr *addr, socklen_t *addrlen);
```

- 클라이언트 소켓의 연결 요청을 수락한다.
- 3가지 인자
  - sock: 서버 소켓(리스닝 소켓)의 디스크립터 번호
  - *addr: 대기 큐를 참조해서 얻은 클라이언트의 주소 정보
  - addrlen: addr 변수의 길이



### send()

```c
ssize_t send(int sockfd, const void * buf, size_t nbytes, int flags);
```

- 연결된 소켓을 통해서 데이터를 보낸다.
- 4가지 인자
  - sockfd: 데이터를 보낼 연결 상태의 소켓
  - buf: 전송할 데이터를 저장한 버퍼의 주소 값
  - nbytes: 전송할 바이트 수
  - flags: 데이터 전송 시 적용할 다양한 옵션 정보



### recv()

```c
ssize_t recv(int sockfd, void * buf, sizt_t nbytes, int flags);
```

- 연결된 소켓을 통해서 데이터를 받는다.
- 4가지 인자
  - sockfd: 데이터를 수신할 연결 상태의 소켓
  - buf: 수신된 데이터를 저장할 버퍼의 주소 값
  - nbytes: 수신할 수 있는 최대 바이트 수
  - flags: 데이터 수신 시 적용할 다양한 옵션 정보



### close()

- 데이터 송수신을 완료한 후 소켓을 소멸시킨다.
- 커널이 해당 소켓의 자원을 모두 시스템에서 제거한다.





### 참고

https://mangkyu.tistory.com/48

https://reakwon.tistory.com/81

https://velog.io/@minji/%EC%86%8C%EC%BC%93%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-bind-listen-accept

https://94kimseongjun.tistory.com/68

https://ddongwon.tistory.com/71

