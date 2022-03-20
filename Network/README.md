# 단권화

## OSI 7 Layer

- 예전에는 네트워크 간 데이터를 통신을 위한 규약이 존재하지 않아, 같은 벤더사의 제품끼리만 통신이 가능했다.
- 이를, 표준화하여 규약으로 만든게 OSI 7 계층이며, 각 계층은 모듈화 되어 있어 독립적인 관계를 가진다.

### 응용 계층(Application)

- 애플리케이션 간 데이터를 전달하기 위한 계층입니다.
- 데이터의 종류에 따라, HTTP, FTP 등의 프로토콜이 사용됩니다.

### 표현 계층(Presentation)

- 데이터의 크기를 줄이기 위해 압축을 선택적으로 할 수 있습니다.
- 데이터의 포맷(JPG, PNG)를 결정하며, 인코딩/디코딩 작업을 수행합니다.

### 세션 계층(Session)

- 네트워크 간 세션을 연결, 유지, 종료를 관리합니다.
- 세션 연결은 **포트** 기반으로 진행됩니다.

### 전송 계층(Transport)

- 포트 주소를 기반으로 다른 네트워크에 **특정 응용프로그램**에 데이터가 정확하게 보내기 위한 계층입니다.
- 데이터의 정확성을 보장하기 위해서는 TCP, 효율성을 보장하기 위해서는 UDP 프로토콜이 사용됩니다.

### 네트워크 계층(Network)

- IP 주소를 기반으로 라우터를 통해 다른 네트워크 상의 컴퓨터에게 데이터를 전달하기 위한 계층입니다.
- 여기서, 라우팅은 데이터 전달을 위해 최적의 경로를 찾는 행위를 의미합니다.

### 데이터 링크 계층(Data Link)

- MAC 주소를 기반으로 LAN 상에서 다른 컴퓨터에게 데이터를 전달하기 위한 계층입니다.
- 데이터 전송 과정에서 오류가 있으면 재전송을 합니다.

### 물리 계층(Phsyical)

- 헤더 및 트레일러가 포함된 비트열을, 내장된 랜카드를 통해 전기 신호로 변환하여 데이터를 전송합니다.

### 세그먼트(Segment)

- 전송계층에서 데이터에 TCP헤더 혹은 UDP가 추가된 데이터를 의미합니다.
- TCP 헤더에는 출발지 포트, 도착지 포트, 버퍼 크기를 나타내는 윈도우 사이즈, 3-way 핸드셰이크를 위한 부호 비트가 있습니다.

### 패킷(Packet)

- 네트워크 계층에서 IP 헤더가 추가된 세그먼트를 의미합니다.
- IP 헤더에는 출발지 및 도착지 IP 주소가 있어, 이를 통해 다른 네트워크의 컴퓨터와 통신을 할 수 있습니다.

### 프레임(Frame) - 데이터 링크

- 데이터 링크 계층에서 이더넷 헤더 및 이더넷 트레일러가 추가된 패킷을 의미한다.
- 이더넷 헤더에는 출발지, 도착지 MAC 주소가 있어 LAN 상에서 도착지 컴퓨터를 찾을 수 있다.
- 단, MAC 주소가 자신의 MAC주소와 다른 경우 역캡슐화를 하지 않고 데이터를 파기한다.
- 수신측이 가지고 있는 FCS와 송신 프레임의 FCS의 동일 여부를 파악하여 에러 여부를 확인한다.

### 데이터그램 vs 패킷이 무슨 차이가 있는지?

- 데이터 그램 : UDP 헤더가 붙은 세그먼트
- 패킷 : TCP 헤더가 붙은 세그먼트

## HTTP

- 클라이언트와 서버가 애플리케이션 계층에서 데이터 전달을 위한 프로토콜입니다.
- HTTP는 상태 및 연결을 유지 하지 않아 스케일 아웃에 유리하며, 송신자, 수신자를 별도로 검증하지 않아 보안적인 이슈가 발생할 수 있습니다.

## GET vs POST

- GET은 자원을 요청하는 메소드입니다.
- POST는 GET과 달리, 자원을 전달하여 서버 상에서 특정 행위를 하는 메소드입니다.
- GET은 멱등성을 보장하는 반면, POST는 멱등성을 보장하지 않습니다.

## HTTP 요청, 응답 헤더

- HTTP 요청(Request) 헤더는 서버로 데이터를 전달하거나, 데이터를 요청할 때 원하는 정보를 담는다.
- HTTP 응답(Respoonse) 헤더는 HTTP 요청에 대한 응답이 담겨 있다.
- 예를 들어, 상태 코드로 요청의 성공 여부를 확인한다.

## HTTP VS HTTPS

- HTTP는 송신, 수신자를 별도로 확인하지 않아 위장의 위험이 있습니다. 그리고, 메시지 바디를 암호화하지 않고, 메시지의 완정성을 보장하지 않기 때문에 변조의 위험이 있습니다.
- 이를 해결하기 위해, 표현 계층의 SSL 혹은 TLS 프로토콜을 통해 데이터를 암호화하여 데이터의 도청 및 변조를 방지할 수 있다.
- HTTPS를 사용하면 브라우저에서 SEO의 점수가 높아지며, 데이터 전송간 보안을 확보할 수 있습니다. 하지만 SSL 핸드셰이크 및 데이터 전송 과정에서 복호화 및 암호화의 오버헤드가 발생합니다.

> Q. HTTPS를 사용하면 헤더도 암호화가 되나요??
> 

## HTTPS 동작 원리

- 비대칭키는 대칭키에 비해 안전하지만 속도가 느리다. 그렇기 때문에, 데이터를 주고 받는 과정에서 비대칭키를 사용한다면 성능 이슈로 이어질 수 있음. 이를 해결하기 위해, 연결 과정에서는 비대칭키를, 데이터를 주고 받는 과정에서는 대칭키로 암호화 하여 통신한다.
- 그렇다면, 어떻게 클라이언트와 서버간에 대칭키를 안전하게 전달할지가 중요하다.
- CA가 존재하는 이유는, **서버의 공개키가 과연 진짜 서버의 것인지를 확인하는 것**이다.

## TSL/SSL handshake

1. 클라이언트 → 서버 : SSL 통신을 시작하며, 클라이언트의 SSL 버전, 암호화 알고리즘, 키 크기 등에 대한 정보를 보냄
2. 서버 → 클라이언트 : SSL 통신이 가능한 경우, 클라이언트로 부터 받은 암호화 알고리즘, 키 크기, SSL 버전 등을 결정하여 응답함.
3. 서버 → 클라이언트 : 공개키 증명서를 보냄
4. 서버 → 클라이언트 : SSL 네고시에이션 종료
5. 최초 네고시에이션 과정이 종료 후, 서버의 공개키로 암호화 한 Pre-Master secret 키를 전달하여 서버가 올바르게 복호화 할 수 있는지 확인합니다.
6. 서버가 Pre-Master secret 키를 제대로 복호화 할 수 있다면, master secret 키를 전달하여 이후 통신은 해당 공통키로 데이터를 암호화 하여 통신을 진행합니다.

## REST

- Representational State Transfer의 약자이며, URI와 HTTP 메소드를 통해 객체화된 서비스를 제공하는 것이다. REST는 리소스, 메서드, 메시지로 구성됩니다.
- REST에서는 주로 메소드로 GET, POST, DELETE, PUT 을 사용한다.
- 예를 들어, `**“신규 회원 임재욱을 생성했습니다”**`
    - 리소스 : 회원
    - 메소드 : 생성
    - 메시지 : 신규 회원 임재욱

## RESTful API

- URI을 아래의 규칙에 맞게 설계했는지를 통해 확인할 수 있다.
    - 명사를 사용하며, 리스트는 복수형을 사용한다. user-users
    - URI에는 행위가 아닌 **자원을 기입**한다.
- 물론 RFC에 표준으로 등록된 내용은 아니다.