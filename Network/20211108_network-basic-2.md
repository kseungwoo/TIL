> 이석복 교수님의 [컴퓨터네트워크](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>



## 네트워크 계층 모델 3가지

<img src="https://user-images.githubusercontent.com/71204049/140693796-196cb7e5-82c8-4132-9fab-5f8f47472f5e.png" width="600" />



- **네트워크 계층 모델**
  - 네트워크 프로토콜 디자인과 통신을 여러 계층으로 나누어 정의
  - 계층별로 역할을 분리
  - 각 계층이 독립적으로 기능 수행
  - 계층 간 통신을 통해 전체 통신 프로세스를 이룬다.
  - 장점
    - 네트워크 통신 과정 단계별로 파악
    - 문제 발생 시 문제 발생 계층을 빠르게 진단할 수 있음.
    - H/W와 S/W를 표준화함으로써 서비스나 기기 간 호환을 가능하게 한다.
- **OSI(Open Systems Interconnetion Reference Model)**
  - 다양한 컴퓨터 시스템이 표준 프로토콜을 사용하여 통신할 수 있도록 국제 표준화 기구(ISO)에서 만든 개념 모델
  - 7계층
- **TCP/IP Model**
  - 미국 국방부(DoD)에서 정의한 현재 산업 표준 네트워크 통신 모델이다.
    - TCP/IP가 OSI보다 더 먼저 사용되었기 때문
  - 4계층 / 5계층(Updated)



## TCP/IP 5계층 모델

#### L5 - Application Layer(응용 계층)

- 프로그램 구현체와 사용자 인터페이스를 의미
- OS에서 제공하는 TCP/UDP 기반의 응용 프로그램을 구현할 때 사용
- Protocol Data Unit
  - Message
- Protocol
  - HTTP, SMTP, FTP, SSH, POP



#### L4 - Transport Layer(응용 계층)

- Process-to-Process Delivery
  - Port 번호를 사용해 최종 도착지인 프로세스까지 데이터를 전달
  - OS 커널에서 구현
- Addressing
  - Port Number
- Protocol Data Unit
  - Segment, Datagram
- Protocol
  - TCP, UDP



#### L3 - Network Layer(네트워크 계층)

- Host-to-Host Delivery
  - 라우팅(Routing)과 포워딩(Forwarding)을 수행해서 목적지 IP 주소까지 패킷을 전달한다.
  - OS 커널에 구현
  - URL이 주어지면 DNS를 통해 IP주소를 찾고 실제 패킷은 IP 주소를 향해 전송된다.
  - IP 주소의 광역대에 따라 Routing Table에 지정된 경로로 패킷을 Forwarding한다.
- Addressing
  - IP Address
- Protocol Data Unit
  - Packet
- Protocol
  - IP
    - Internet Potocol Address
    - Host의 논리적 주소로, 전 세계의 네트워크 상에서 유일하다.
    - IPv4는 4byte, IPv6은 8byte 주소를 갖는다.



#### L2 - Data-Link Layer(데이터 링크 계층)

- 1-hop delivery
  - 라우팅(Routing)과 포워딩(Forwarding)을 수행해서 목적지 MAC 주소까지 프레임을 전달한다.
  - 인접 노드들 간의 신뢰할 수 있는 전달
  - Ethernet Card에 구현
- Addressing
  - MAC Address
    - Media Access Control Address
    - Ethernet Card의 물리적 주소, 로컬 네트워크 안에서만 유일
    - Gateway(라우터)는 Ethernet Card를 2개 가지며, LAN과 WAN을 연결
- ARP
  - Address Resolution Protocol
  - LAN 내부의 ARP Table을 참조하여 IP 주소를 MAC 주소로 변환
- Protocol Data Unit
  - Frame
- Protocol
  - IEEE 802, Ethernet, Wi-Fi



#### L1 - Physical Layer(물리 계층)

- Encoding: 0과 1의 디지털 신호를 아날로그 신호로 변환하여 전송
- Decoding: 아날로그 신호를 0과 1의 디지털 신호로 해석
- Hardware에 구현



(사진 및 내용 출처: [티스토리](https://velog.io/@jwkim/cs-nw-osi-tcp-ip))



