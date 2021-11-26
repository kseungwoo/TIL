> [티스토리 글](https://dev-gorany.tistory.com/235)을 읽고 정리하였습니다. 

## Websocket이란

- Websocket은 단일 tcp 연결을 통해 클라이언트와 서버 간의 전이중 양방향 통신(Full Duplex 2-way Communication) 채널을 설정하는 표준화된 프로토콜이다.
- HTTP와 다른 프로토콜이지만, 80(HTTP), 443(HTTPS) 포트를 사용하고, 기존 방화벽 규칙을 재사용할 수 있도록 HTTP를 기반으로 설계되었다.

## STOMP란

- STOMP(Simple Text Oriented Messaging Protocol)은 메시지 전송을 효율적으로 처리하기 위해 탄생한 프로토콜이다. 
- 메시지 브로커(Rabbit MQ, Active MQ 등)를 사용하여 메시지 Pub/Sub(발행 및 구독) 서비스를 이용할 수 있다.
  - Pub/Sub(발행 및 구독)이란 메시지를 발행하는 주체와 소비하는 주체를 분리해 제공하는 메시징 방법이다.
- 즉, Websocket 위에서 동작하는 프로토콜로써 클라이언트와 서버가 전송할 메시지의 유형, 형식, 내용들을 정의하는 메커니즘이다.



## SockJS 

**SockJS**를 사용하면 WebSocket을 지원하지 않는 웹 브라우저에서도 WebSocket Emulation을 이용해 웹소켓을 이용하는 것 처럼 동작하게 해준다.



## WebSocket과 STOMP를 구분하자.

서버-클라이언트 구조는 일반적으로 클라이언트가 서버에 요청을 보내면, 서버는 그 요청을 받아 로직을 처리한 후 클라이언트에 응답하는 방식이다.

그런데 웹소켓을 사용하면 클라이언트의 요청 없이도 서버가 데이터를 클라이언트에 보낼 수 있다. 예를 들어, 클라이언트가 채팅을 서버에 보내면 서버는 다시 클라이언트들에게 데이터를 보내는 것이다.

여기서 STOMP를 추가적으로 사용한다면, pub/sub 구조를 사용할 수 있다. STOMP를 사용하기 이전에는 WebSocketSession에 직접 메시지를 전달해줘야 했다면, 이제는 특정 패턴(문자열)을 구독함으로써 WebSocketSession을 직접 다루지 않고서도 채팅방을 고도화할 수 있다는 것이다.

STOMP에 내장하는 Broker의 역할에 대해 알아보자. 클라이언트가 서버에 메시지를 보내면 서버는 메시지에 특정 패턴을 심어 Broker에게 전달한다. 그러면 Broker는 해당 패턴을 구독하고 있는 클라이언들에게 메시지를 전달해준다. 여기서 Broker는 외부 Message Broker(RabbitMQ, ActiveMQ)를 사용해도 된다.



