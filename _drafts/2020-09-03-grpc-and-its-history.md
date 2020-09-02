---
title:  "등장배경으로 알아보는 gRPC 101"
excerpt: "대 MSA 시대에 딱 맞는 기술인 gRPC가 어떻게 등장하게 되었나"
toc: true
toc_sticky: true

categories:
-  Study
tags:
-  Network
last_modified_at: 2020-09-03TO20:30:00+09:00
---

현재 공유기로 묶여 있는 라즈베리파이에, 서버가 요청을 보내는 것을 구현해야한다.
하지만 사설망에 있으면? 라즈베리파이에서 서버로 요청을 보내야 하고,
세션을 유지하는 방식으로 진행해야한다.

기본 지식이 부족한 것 같아서 공부하였고,
내용을 정리해본다 (TIL)

### TCP vs UDP

> TCP UDP 비교 표

- TCP는 TCP/IP의 TCP가 맞다.

- TCP UDP는 전송 계층 프로토콜이다

- OSI - TCP/IP 그림

### HTTP/1, 2 TCP

### HTTP/3 UDP (QUIC)

### Socket programming

- 소켓이 인스턴스
- TCP, UDP가 추상적인 프로토콜인 것이다.

TCP programming
TCP 연결과 같은 과정을 서버가 해주는 것이다.

### 우리 과정

백엔드가 세션 정보를 잃어버렸어 또다시 연결할 방법이 ㅇ벗다.
TCP connection은 상시 연결되어 있어야함
udp로는 만들 수 없다. TCP로 해야한다.
