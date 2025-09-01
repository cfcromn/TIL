## WebSocket이란?

클라이언트와 서버 간의 메시지를 교환하기 위한 통신 방법 중 하나로 2011년 RFC 6455에 의해 표준화됨

WebSocket을 지원하는 브라우저는 WebSocket Protocol을 지원한다.

## WebSocket 이전 HTTP를 이용한 실시간 통신 기능

- Poling
    - 클라이언트가 서버에 일정한 주기로 요청을 지속적으로 송신한다.
    - 불필요한 요청 생성으로 인한 오버헤드가 발생할 수 있다.

- Long Poling
    - 클라이언트가 서버에 요청을 보낸 뒤, 응답을 수신할 때까지 연결을 종료하지 않고 대기한 뒤 응답 시 연결을 끊고 다시 요청
    - 통신의 양이 많아질 경우 Poling 방식과 유사해진다.
    
- Streaming
    - 클라이언트가 서버에 요청을 보내면, 연결을 유지한 상태로 서버로부터 지속적인 응답을 수신한다
    - 클라이언트에서 서버로의 데이터 송신이 어렵다

## WebSocket의 특징

- 양방향 통신 (Full-Duplex)
    - 데이터를 송/수신을 동시에 처리할 수 있다
    - 단방향 통신인 HTTP 통신과 달리 클라이언트와 서버가 서로 원하는 순간에 데이터를 주고 받을 수 있음
- 실시간 네트워킹 (Real-Time Networking)
    - 연속된 데이터를 빠르게 노출 시킬 수 있다
    - 여러 단말기에 빠르게 데이터를 교환할 수 있다.
    

## WebSocket 동작 과정

![image.png](attachment:4f8c72ae-1b39-44b4-822c-323c0c3a727c:image.png)

WebSocket의 동작 과정은 **Opening Handshake, Data transfer, Closing Handshake  이렇게 3가지로 나눌 수 있다.**

## Handshake

- Opening Handshake와 Closing Handshake는 일반적인 HTTP TCP 통신의 과정 중 하나이다.

### 요청(Request) 헤더

**GET/chatHTTP/1.1**

웹소켓의 통신 요청에서 HTTP 버전은 1.1 이상이어야 하고 GET 메서드를 사용한다.

**Upgrade**

프로토콜을 전환하기 위해 사용하는 헤더

웹소켓 요청 시 반스에 websocket 이라는 값을 가지며, 이 값이 없거나 다른 값일 경우 cros-protocol attack이라고 간주하여 웹소켓 접속을 중지시킨다.

**Connection**

현재의 전송이 완료된 후 네트워크 접속을 유지할 것인가에 대한 정보이다

웹소켓 요청 시에는 반드시 Upgrade라는 값을 가진다.

Upgrade와 마찬가지로 이 값이 없거나 다른 값이면 웹소켓 접속을 중지 시킨다.

**Sec-WebSocket-Key**

유효한 요청인지 확인하기 위해 사용하는 키 값

**Sec-WebSocket-Protocol**

사용하고자 하는 하나 이상의 웹소켓 프로토콜 지정 (필요한 경우에만 사용)

**Sec-WebSocket-Version**

클라이언트가 사용하고자 하는 웹소켓 프로토콜 버전

**Origin**

CORS 정책으로 만들어진 헤더

Cross-Site WebSocket Hijacking과 같은 공격을 피하기 위한다.

### 응답(Response) 헤더

**HTTP/1.1 101 Switching Protocols**

101은 HTTP에서 WS로 프로토콜 전환이 승인 되었다는 응답코드이다.

**Sec-WebSocket-Accept**

요청 헤더의 Sec-WebSocket-Key에 유니크 아이디를 더해서 SHA-1로 해싱한 후 base64로 인코딩한 결과이다.

웹 소켓 연결이 개시되었음을 알린다.

## Date Transfer

Opening HandShake에서 승인이 나면, 웹소켓 프로토콜로 노란색 박스 부분인 Date Transfer가 진행된다.

여기서 데이터는 messsage라는 단위로 전달된다

**Messsage**

여러 프레임(Frame)이 모여서 구성되는 하나의 논리적인 메세지 단위

**Frame**

데이터 링크 계층에서 주고 받는 가장 작은 단위의 데이터

작은 헤더 + payload로 구성되어 있다.

## Closing Handshake

- 클라이언트 혹은 서버가 상대방에게 연결 종료를 위한 Close Frame을 전송한다
- 요청을 받은 쪽에서 응답으로 Close Frame을 전송하여 Web Socket 연결 종료한다

## Socket.io, SockJS

- HTML5 이전의 기술로 구현된 서비스에서 WebSocket과 유사한 실시간성을 보장하도록 지원
- 여러 실시간 통신 기법들을 하나의 API로 추상화한 뒤, 브라우저와 웹 서버의 종류, 버전을 파악하여 가장 적합한 기술을 선택하여 사용한다.
    - WebSocket, FlashSocket, AJAX Long Polling, AJAX Multipart Streaming, IFrame, JSONP Polling 등