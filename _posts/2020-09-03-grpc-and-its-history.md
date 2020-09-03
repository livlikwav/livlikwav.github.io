---
title:  "REST를 위협하는 gRPC의 등장배경과, HTTP/2를 비롯한 특징들"
excerpt: "socket->RPC->REST->gRPC"
toc: true
toc_sticky: true

categories:
-  Study
tags:
-  Network
last_modified_at: 2020-09-03TO20:30:00+09:00
---

## gRPC 소개

![gRPC](https://grpc.io/img/logos/grpc-logo.png)
> A high-performance, open source universal RPC framework

참고한 영상에 따르면,
구글이 **1주일 동안 띄우는 컨테이너가 20억개**에 달한다고 한다.
또한, 구글이 **1초 동안 던지는 원격 호출의 수는 100억번**이라고 한다(2017년 영상 기준)

구글은 MSA로 이런 거대한 서비스를 운영하고 있고,
이를 위해 stubby라는 내부 RPC 프레임워크를 이미 예전부터 사용하고 있었고,
이를 기반으로 오픈소스로 만든 RPC 프레임워크가 바로 gRPC이다.

2016년 8월에 1.0.0이 출시된 나름 따끈한(?) 기술이다.
구글, 넷플릭스, 시스코 등의 해외 기업과,
버즈빌, 뱅크샐러드 등의 한국 기업도 이미 사용하고 있는 것 같다.

## 참고한 링크

- [[NBP 기술&경험] 시대의 흐름, gRPC 깊게 파고들기 #1](https://blog.naver.com/n_cloudplatform/221751268831)
- [[NBP기술&경험]시대의 흐름, gRPC 깊게 파고들기 #2](https://blog.naver.com/n_cloudplatform/221751405158)
- [google - HTTP/2 소개](https://developers.google.com/web/fundamentals/performance/http2?hl=ko)
- [스프링캠프 2017 [Day1 B5] : gㅏ벼운 RPC, gRPC(빠르고 가벼운 Polyglot RPC framework)](https://www.youtube.com/watch?v=sKWy7BJxIas&t=2447s)

## gRPC 이전의 배경

> 네이버 클라우드 플랫폼 블로그 글이 많은 도움이 되었다.

### 서버-클라이언트 모델과 IPC의 필요성

Server-Client Model

- PC(personal computer) 개념이 없던 시절
  - 프로그램은 하나의 메인 프레임에서 동작하는 monolithic 구조로 설계되었다
- 하지만 메인 프레임워크는 매우 고가였다.
- 기술 발전에 따라 소형 컴퓨터 장비들이 등장하였다.(상대적으로 저가)
- 따라서 메인 프레임워크 1대의 기능을 여러 워크스테이션 서버로 묶어서 사용하고 싶어했다.
  - 이 결과로 Server-Client Model이 등장하였다.
- 메인 프레임워크의 기능을 워크스테이션 서버로 분산, 네트워크 연결로 서비스
  - 서버-서버 혹은 서버-PC 간 네트워크 연결/통신 중요해짐
  - 따라서 네트워크 계층 구조 정의되고 발전함
    - OSI 7 layer, TCP/IP 등

IPC = Inter Process Communication

- 네트워크 간 통신은, 실질적으로 로컬 컴퓨터 프로세스-원격지 컴퓨터 프로세스가 IPC 통신을 하는 것이다.
- 이러한 **IPC 기법으로 소켓, RPC, REST, gRPC등의 기술들이 발전해온 것이다.**

### gRPC 이전의 Socket->RPC->REST

> IPC 기법에는 공유 메모리, PIPE, 메시지 큐 등 소켓 외에도 여러가지가 있다.

- Socket
  - OSI 7 layer 구조의 Application Layer에서 Transport Port의 TCP, UDP를 이용하기 위한 수단
  - 장점
    - 대부분의 언어에서 API 형태로 제공하여 편리함
  - 단점
    - 일련의 통신 과정을 직접 구현하므로 통신 관련 장애 처리도 개발자의 몫이다.
    - 서비스가 고도화될 수록 data formatting도 점점 어려워짐.
  - 이러한 **소켓의 한계에서 RPC가 등장함.**

- RPC
  - Remote Procedure Call
  - 네트워크로 연결된 서버 상의 프로시저(함수, 메서드)를 원격으로 호출할 수 있는 기능
  - 장점
    - 네트워크 통신 작업 신경 안써도됨(통신, call 방식등)
    - IDL 기반으로 다양한 언어를 가진 환경에도 쉽게 확장 가능
    - 인터페이스 협업에도 용아함(IDL)
  - 단점
    - **사용하기 편리한 구현체가 없었음**
    - 구현의 어려움
    - 지원 기능의 한계
  - 데이터 통신을 우리에게 익숙한 Web을 활용 해보려는 시도로 이어져 REST가 등장함.

- REST
  - REpresentational State Transfer
  - HTTP/1.1 기반
    - URI를 통해 모든 자원 명시
    - HTTP Method를 통해 처리하는 아키텍쳐
  - 장점
    - 자원 그 자체를 표현하기에 직관적
    - HTTP 그대로 계승하였기 때문에 별도 작업 없이 쉽게 사용 가능
  - 단점
    - 표준이 아니기 때문에 parameter와 응답 값이 명시적이지 않다.
    - HTTP 메소드가 제한적이기 때문에 세부 기능 구현에 제약이 있다.
    - 웹 데이터 전달 format 상의 문제
      - string 기반이라 별도의 serialization 필요
      - XML
        - 비효율적인 데이터 구조탓에 속도 느림
      - JSON
        - 제공되는 자료형의 한계로 파싱 후 추가 형변환 필요

REST가 보편적으로 사용던 중, google 사에서 개발한 오픈소스 RPC 프레임워크인 gRPC가 등장하게 된다.

## gRPC

RPC는 사실 예전부터 존재했던 기술이다. 하지만 **이렇게 띠용하는 기술이 없었을 뿐.**

**Docker처럼,** 이전에 리눅스 컨테이너 기술(자원 격리 기술)이 이미 존재했지만, 너무 사용하기 어려워서 보편적으로 안쓰였던 것과 유사하다.

### RPC 구조

![rpc-structure](https://postfiles.pstatic.net/MjAxOTEyMTlfMTMy/MDAxNTc2NzM1MTk3MDgy.WRcx_IzWZKQAHZ2st9oWFdIem4z75gkFO-JqiBjmppgg.rNgZciIZLxuTef8fuQJpVYoZlTcw8FNmJwEd1bXzwoAg.PNG.n_cloudplatform/1.png?type=w966)

키워드

- **Stub (RPC의 핵심)**
  - 서버와 클라이언트간 함수 호출에 사용된 매개 변수 변환을 담당함
- Marshalling
  - 함수 호출에 사용된 파라미터 변환
- Unmarshalling
  - 서버가 사용하기 위해, 클라이언트가 전달한 매개 변수의 역변환
- Client stub
  - Marshalling
  - 함수 실행 후 서버에서 전달된 결과의 변환
- Server stub
  - Unmarshalling
  - 함수 실행 결과 변환

기본적인 RPC의 통신 과정

- IDL(Interface Definition Language)을 사용하여 호출 규약 정의합니다.
  - 함수명, 인자, 반환값에 대한 데이터형이 정의된 IDL 파일을 rpcgen으로 컴파일하면 stub code가 자동으로 생성됩니다.
- Stub Code에 명시된 함수는 원시코드의 형태로, 상세 기능은 server에서 구현됩니다.
  - 만들어진 stub 코드는 클라이언트/서버에 함께 빌드합니다.
- client에서 stub 에 정의된 함수를 사용할 때,
- client stub은 RPC runtime을 통해 함수 호출하고
- server는 수신된 procedure 호출에 대한 처리 후 결과 값을 반환합니다.
- 최종적으로 Client는 Server의 결과 값을 반환받고, 함수를 Local에 있는 것 처럼 사용할 수 있습니다.

![grpcoverview](https://grpc.io/img/landing-2.svg)
> gRPC도 구조가 다르지 않다. RPC의 구현체 중 하나이기 때문.

### gRPC의 특징

1. HTTP/2를 사용한다
   1. (REST는 보통 HTTP/1.1을 사용한다)
   2. 헤더 압축
   3. 서버 푸시 지원(클라이언트 요청 한번에 서버 응답 여러번 가능)
   4. 메시지 인터리빙 허용 등 장점이 많다.
   5. (사실 이젠 HTTP/3 버전이 생겼다. HTTP/2가 최신은 아님)
2. Protocol Buffer로 데이터를 전달한다
   1. JSON, XML로 데이터 전달하는 것에 비해 크기를 획기적으로 줄인다.
   2. 밑의 예제에서 json은 82byte인데 이를 33byte로 줄인다.
3. Proto File로 서비스와 메시지를 정의하고, 여러가지 언어로 코드를 자동 생성한다.
   1. grpctools-protoc으로 코드 생성
   2. polyglot(약 10가지 언어 지원)

![http2](https://postfiles.pstatic.net/MjAxOTEyMTlfMjM4/MDAxNTc2NzM1MjU1ODc3.XB2ldLI8SUdIi2XmB1WJ8VRyekjzDZvBE2Oa-LDidpwg.AICWtHri0jrx9DAe9zSlBcwI0B42qu5Z8MLM84L_UzYg.PNG.n_cloudplatform/2.png?type=w966)
> HTTP/1.1 vs HTTP/2

![protobuffer](https://postfiles.pstatic.net/MjAxOTEyMTlfMTQw/MDAxNTc2NzM1MjkwMDE2.nt68WH1RW0sgwbj_OVZtV1g56to7lpEH6ES6kxA-txAg._B_Sguop8b4BBo2TdPf1G2U0I-UB17tE8XPNBQ3tzIYg.PNG.n_cloudplatform/3.png?type=w966)
> JSON vs Protocol Buffer 데이터 비교

### gRPC의 단점

현재 **브라우저에서 사용할 수는 없는 것 같다.**
따라서 백엔드에서 **서버-서버 통신**에 자주 사용되고, **MSA**에서 자주 사용된다.
