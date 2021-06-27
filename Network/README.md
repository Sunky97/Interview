# 네트워크
🔖 Contents
- [OSI 7계층](#OSI-7계층)
- [TCP/IP 개념](#TCP/IP-개념)
- [TCP 와 UDP](#TCP-와-UDP)
- [HTTP 와 HTTPS](#HTTP-와-HTTPS)
- [쿠키와 세션](#쿠키와-세션)
- [DNS](#DNS)
- [REST 와 RESTful](#REST-와-RESTful)

<hr>

## OSI 7계층

![osi7layer](https://media.vlpt.us/images/dyllis/post/7a6679e2-26e0-4d3e-b792-c866b9012226/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.png)

1. 물리 계층(Physical Layer)
    - 네트워크의 기본 네트워크 하드웨어 전송 기술을 이룬다.
    - 네트워크의 높은 수준의 기능의 논리 데이터 구조를 기초로 하는 필수 계층이다.
    - 전송 단위는 Bit이다.
2. 데이터 링크 계층(Data Link Layer)
    - 포인트 투 포인트(Point to Point) 간 신뢰성있는 전송을 보장하기 위한 계층으로 CRC 기반의 오류 제어와 흐름 제어가 필요하다.
    - 주소 값은 물리적으로 할당 받는데, 이는 네트워크 카드가 만들어질 때부터 맥 주소(MAC address)가 정해져 있다는 뜻이다.
    - 데이터 링크 계층의 가장 잘 알려진 예는 이더넷이다.
    - 데이터 전송 단위는 Frame이다.
3. 네트워크 계층(Network Layer)
    - 여러개의 노드를 거칠때마다 경로를 찾아주는 역할을 하는 계층으로 다양한 길이의 데이터를 네트워크들을 통해 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 제공하기 위한 기능적, 절차적 수단을 제공한다.
    - 네트워크 계층은 라우팅, 흐름 제어, 세그멘테이션(segmentation/desegmentation), 오류 제어, 인터네트워킹(Internetworking) 등을 수행한다.
    - 논리적인 주소 구조(IP), 곧 네트워크 관리자가 직접 주소를 할당하는 구조를 가지며, 계층적(hierarchical)이다.
    - 데이터 전송 단위는 Datagram(Packet)이다.
4. 전송 계층(Transport Layer)
    - 양 끝단(End to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 해 주어, 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해준다.
    - 시퀀스 넘버 기반의 오류 제어 방식을 사용한다.
    - 전송 계층은 특정 연결의 유효성을 제어하고, 일부 프로토콜은 상태 개념이 있고(stateful), 연결 기반(connection oriented)이다. (이는 전송 계층이 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송한다는 것을 뜻한다.)
    - 가장 잘 알려진 전송 계층의 예는 TCP이다.
    - 데이터 전송 단위는 Segment이다.
5. 세션 계층(Session Layer)
    - 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공한다.
    - 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신과 함께, 체크 포인팅과 유휴, 종료, 다시 시작 과정 등을 수행한다.
    - 이 계층은 TCP/IP 세션을 만들고 없애는 책임을 진다.
6. 표현 계층(Presentation Layer)
    - 코드 간의 번역을 담당하여 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어 준다.
    - MIME 인코딩이나 암호화 등의 동작이 이 계층에서 이루어진다.
7. 응용 계층(Application Layer)
    - 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.
    - 일반적인 응용 서비스는 관련된 응용 프로세스들 사이의 전환을 제공한다.

## TCP/IP 개념

#### TCP/IP 는 프로토콜의 집합

TCP/IP는 하나의 프로토콜을 지칭하는 말이 아니라 인터넷에서 사용되는 각종 표준 프로토콜을 한데 모아 일컫는 말이다. 흔히 TCP/IP 라고 부르는 이유는 TCP와 IP가 이들 프로토콜 중 가장 대표적인 프로토콜이기 때문이다. 각각의 개별 프로토콜을 일컫는 말이 아니라. 인터넷 프로토콜 집합의 의미로 굳이 구분해야 할 때에는 TCP/IP 프로토콜 스위트라고 부르거나 인터넷 프로토콜 스위트 라고 부르면 된다.

## TCP 와 UDP

- (https://sunky97.github.io/network/tcp-udp/)

## HTTP 와 HTTPS
- (https://sunky97.github.io/network/http-https/)

## 쿠키와 세션

- 쿠키(Cookie)는 클라이언트에 저장되는 작은 데이터, 보안에 취약함, 속도가 빠름, 브라우저를 종료해도 계속해서 남아 있을 수 있다.
- 세션(Session) 서버에 저장되는 데이터로, SessionID 를 식별자로 사용해서 서버에 데이터를 저장함. 보안에 강함, 속도가 느림, 브라우저가 종료되면 만료시간에 상관없이 삭제

## DNS

- DNS(Domain Name System)
    - 범국제적 단위로 웹사이트의 IP 주소와 도메인 주소를 이어주는 환경/시스템

## REST 와 RESTful

#### REST란?
- REST 란 “Representational State Transfer” 의 약자이다. 월드 와이드 웹과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식이다.
- REST란, “웹에 존재하는 모든 자원(이미지, 동영상, DB 자원)에 고유한 URI를 부여해 활용”하는 것으로, 자원을 정의하고 자원에 대한 주소를 지정하는 방법론을 의미한다고 한다.
- 이런 REST의 형식을 따른 시스템을 `RESTful` 이라고 부른다.
- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
