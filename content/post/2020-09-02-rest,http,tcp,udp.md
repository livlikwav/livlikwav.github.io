---
categories:
- Study
date: "2020-09-02T00:00:00Z"
excerpt: REST API, 메시지를 컨트롤하는 HTTP, 그리고 패킷을 컨트롤하는 TCP와 UDP
last_modified_at: 2020-09-02TO23:30:00+09:00
tags:
- Network
title: 네트워크 기초 바로잡기 - REST API, HTTP, TCP, 그리고 UDP 개념 정리
toc: true
toc_sticky: true
---

지금 진행중인 프로젝트에서 새로운 기술적인 이슈가 있었다.
현재 서버는 Flask로 REST API를 구성하였다.
그리고 공유기로 구성한 사설망에 클라이언트(라즈베리파이)가 있다.
이 상황에서 서버에서 클라이언트로 Server push하는 방법을 고민중이다.
문제는 서버가 클라이언트 주소를 알 수 없기 때문에 결국 클라이언트에서 요청이 시작되어야 한다.

열심히 구글링을 했고, 일단은 gRPC로 약 5초 간격의 polling 방식으로 구현을 하기로 생각하고 있다.
공부를 하는 과정에서 나는 HTTP와 TCP 조차 헷갈리고 있었고,
따라서 네트워크 기초 지식을 한번 정리하고 넘어가고 싶다 :)

### 참고한 글

- [[WEB] HTTP, TCP/IP, 메시지란?](https://medium.com/@chrisjune_13837/web-http-tcp-ip-%EB%A9%94%EC%8B%9C%EC%A7%80%EB%9E%80-4b2721fe296f)
- [OSI 7 Layer 과 TCP/IP 4 Layer(TCP/IP Protocol suite) 비교](https://goitgo.tistory.com/25)
- [Microsoft - Compare gRPC services with HTTP APIs](https://docs.microsoft.com/ko-kr/aspnet/core/grpc/comparison?view=aspnetcore-3.1)
- [Mozilla - HTTP 개요](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)

### HTTP, TCP, UDP 뭐가 다른거야?

결론적으로,

- HTTP는
  - 메시지를 컨트롤한다
  - OSI 7 계층에서 응용 계층(Application layer, L7)에 해당한다
- TCP와 UDP는
  - 패킷을 컨트롤한다
  - OSI 7 계층에서 전송 계층(Transport layer, L4)에 해당한다.

둘다 프로토콜은 맞지만, 사용되는 역할이 다르다.
네트워크 모델에서의 역할 자체가 다르다.

![OSI vs TCP/IP](https://user-images.githubusercontent.com/44190293/91993635-95965980-ed70-11ea-84d9-477706041efe.png)

위 그림에서 맨 오른쪽 위에서 HTTP를 찾을 수 있고,
중간에 TCP와 UDP를 볼 수 있다.
밑에서 Ethernet이라는 자주 보이는 용어도 볼 수 있다.

### OSI 7 layers와 TCP/IP 4 layers는 뭐가 다른거야?

둘다 네트워크 통신을 추상화한, 계층화된 모델이다(이해하기 쉽도록).
TCP/IP 4 layers는 웹 서비스를 이해하기 쉬운, 더 단순한 모델이다.

> OSI 7 layers를 단순화 시킨 모델이라는 글들이 있는데,
> TCP/IP가 OSI 모델보다 먼저 개발되었다는 글도 있다.
> 그 근거로 두 모델의 계층이 정확하게 일치하지 않는다는 근거를 제시한다.

- 현재 대부분의 통신 프로토콜은 TCP/IP가 사용된다.
- OSI 7 layers는 Reference의 가치가 있다.

TCP/IP Model을 조금 더 살펴보면,

- Application Layer
  - 네트워크를 사용하는 응용프로그램으로 이뤄진다.
- Transport Layer
  - 시스템을 연결하고 데이터를 전송하는 역할을 한다.
- Internet Layer
  - 데이터를 정의하고 데이터의 경로를 라우팅한다.
- Physical Layer
  - 네트워크 하드웨어를 의미한다.

### TCP와 IP의 차이는 뭘까?

- TCP는
  - 데이터의 전달을 관리하는 규칙이다.
- IP는
  - 인터넷 상의 주소 규칙이다.

![ex for tcp/ip](https://user-images.githubusercontent.com/44190293/91995606-fb83e080-ed72-11ea-8dd3-200f08a983c9.png)

TCP/IP 4계층을 통해서 네트워크 통신의 예시를 들면

1. 클라이언트 -> 서버, 특정 주소로 요청
2. DNS 상에서 IP 주소를 받아옴
3. HTTP 계층 -> HTTP 메시지 작성
4. TCP 계층 -> HTTP 메시지를 패킷으로 분해
5. IP 계층 -> 전송 위치를 확인
6. Ethernet 계층 -> 네트워크를 통해서 전송
7. 수신은 위의 과정의 역순으로 진행함.

### HTTP는 TCP를 사용하는 거야?

![http-layers](https://mdn.mozillademos.org/files/13673/HTTP%20&%20layers.png)
> HTTP는 애플리케이션 계층의 프로토콜로, 신뢰 가능한 전송 프로토콜이라면 이론상으로는 무엇이든 사용할 수 있으나 TCP 혹은 암호화된 TCP 연결인 TLS를 통해 전송됩니다.

인용한대로, 다른 전송 프로토콜을 사용할 수 있지만, 대부분 TLS(Secured TCP)를 사용한다.

### REST API는 HTTP를 사용하는 거야?

(내가 이해한 바로는) 지금까지는 대부분 HTTP/1.1을 사용하고 있고, HTTP/2도 적용 가능하다.

![gRPC vs HTTP API](https://user-images.githubusercontent.com/44190293/91995860-456cc680-ed73-11ea-9cf9-d617f1796027.png)
> REST API라고 부르기 위해서의 규칙은 엄격하기 때문에, REST API가 아닌 HTTP API를 용어를 사용하자고 한다. 그 연장선 상에서 HTTP API로 표현했다고 이해했다.

여기서 일단 HTTP API 부분만 보자.

- Protocol
  - HTTP를 사용한다.
  - HTTP method(POST, GET, PUT, DELETE ...)
- Payload(전송의 근본적인 목적이 되는 데이터)
  - JSON을 사용한다.
  - 기본적으로 Text로 전송한다는 의미
- Contract
  - API를 어떻게 사용하는지 규칙을 말하는 것 같다.
  - 말 그대로 옵션이다. (따라서 API 변화에 클라이언트가 영향을 받을 수 있다.)
  - Swagger(OpenAPI)와 같은 도구를 사용해 자동화할 수 있다.

### TCP와 UDP는 뭐가 다른거야?

연결형 서비스 vs 비연결형 서비스.

TCP와 UDP는 둘 다 전송 계층의 프로토콜이다.
시스템을 연결하고 데이터를 정의하는 규칙이다.

패킷 교환 방식의 차이가 연결성을 결정하게 된다.

![tcp vs udp](https://user-images.githubusercontent.com/44190293/91997774-68987580-ed75-11ea-8e2c-775c827b0c98.png)

위 표를 참고하자.

### HTTP는 stateless라는데 이게 비연결형을 말하나?

아니다. stateless는 무상태성이고, HTTP는 연결형 서비스이다.
(보통 TLS(Secured TCP)를 사용하기 때문에)

무상태성은 HTTP 통신에서 서버가 클라이언트의 정보를 저장하지 않음을 말한다.
Connectionless하게 서버가 응답을 마치면 연결을 끊어버린다.

새로운 클라이언트의 요청이 오면, 그때마다 서버는 클라이언트를 확인해야한다.
따라서 HTTP 통신에서는 클라이언트가 매번 HTTP 메시지에 Header를 담아 보낸다.
(이는 곧 HTTP/2의 등장 배경이 된다.)

### 이제 gRPC를 공부할 준비가 됐다

TCP/IP Model로 통신 과정을 이해하고,
HTTP도 무엇인지 이해했다.

gRPC는 HTTP/2를 사용하고, JSON이 아닌 protocol buffer를 이용해 통신한다.
위의 내용을 정리했으니, gRPC의 등장배경을 더 잘 이해할 수 있게 되었다!
