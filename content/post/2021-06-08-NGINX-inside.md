---
categories:
- Study
date: "2021-06-08T00:00:00Z"
excerpt: Apache와 NGINX의 차이, concurrent connections를 위한 event-driven architecture와
  non-blocking I/O
last_modified_at: 2021-06-08TO13:00:00+09:00
tags:
- NGINX
- Event-driven architecture
title: 'NGINX 내부 구조 이해하기: 동시 연결 수와 이벤트 주도 설계'
toc: true
toc_sticky: true
---

## NGINX 내부 구조 이해하기

웹 서버 개발을 한다면, 무조건 자주 보이는 그 이름 NGINX.  
막연하게 Apache보다 가볍고, 성능이 좋다고 알고 있었는데,  
정작 '왜' 가볍고 성능이 좋은지는 파고든 적이 없는 것 같아 나름대로 공부해본 것을 정리한다.  

정확히는 다음과 같은 질문들에서 출발했다.

- NGINX가 apache의 c10k problem을 해결할 수 있었던 이유가 뭐지?
- NGINX가 reverse proxy로 주로 쓰이는 이유는 뭐지? Apache는 그런 기능이 없나?

Apache는 아직 사용해본적이 없는 터라 더 막연했다.  
하지만 역시나 공식 블로그에 다 잘 나와 있었다.  
그리고 이를 실로 이해하기 위해서, 관련된 CS 기초를 먼저 살펴봤다.  
NGINX 공식 블로그 글을 읽기까지, 사실 기초 복습하는 시간이 더 걸린 것 같다.

### 참고한 글

- [Inside NGINX: Infographic](https://www.nginx.com/resources/library/infographic-inside-nginx/)
- [Inside NGINX: How We Designed for Performance & Scale](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)

1번째 링크는 NGINX의 설계를 한 눈에 볼 수 있는 인포그래픽이다.  
2번째 링크는 1번째 인포그래픽을 하나하나 설명해주는 형식의 글이다.

NGINX 블로그에 더 자세한 설명이나 Apache와의 비교 글도 잘 나와있다.

### 먼저 보면 좋은 CS 기초

나는 NGINX 인포그래픽을 먼저 본 후,  
그림에 나오는 `epoll`, `kqueue` 등의 keyword 라던지,  
웹 서버를 구현하는 방법이나 non-blocking I/O 등의 기초 지식들을 먼저 공부했다.

그 중 NGINX 이해에 도움이 되었던 지식들은 다음과 같다.

- 소켓 프로그래밍과 파일 디스크립터
  - socket API(`socket()`, `bind()`, `listen()` ...)
  - listen 소켓과 connection 소켓
- 프로세스, 스레드
- 메모리 영역 구분, IPC와 문맥 교환
- SW, HW 인터럽트와 IRQ lines
- I/O 방식의 변화
  - 블로킹 동기 I/O
  - 논-블로킹 동기 I/O
  - 블로킹 비동기 I/O (`select`)
  - 논-블로킹 비동기 I/O (`epoll`, `kqueue` ...)
- 웹 서버 구현 방식의 변화
  - 멀티 프로세스 -> 멀티 스레드 -> 멀티 플렉싱 I/O

## NGINX가 기존의 웹 서버와 달랐던 점

(본격적인 설명에 앞서, 틀린 내용이 있을 수도 있음을 주의하자. 이 글을 한국어로 빠르게 훑고, 위의 영어 본문을 읽어주시면 감사하겠다.)

내가 정리한 핵심은 이것이다.

- NGINX가 개선한 것
  - **동시에 처리할 수 있는 연결 수를 비약적으로 증가**시킴. (concurrent connections)
- 이를 위해 개선된 설계
  - Event-driven architecture와 non-blocking I/O
- 설계를 구현한 방식
  - 고정된 수의 worker 프로세스만을 관리한다.
  - 이 프로세스는 blocked 되지 않고, listen 소켓과 connection 소켓의 이벤트를 기반으로 non-blocking으로 동작한다.
  - 이를 통해 사용하는 리소스나 문맥 교환 횟수도 현저히 줄인다.

### 기존 웹 서버들의 동작 방식

![blocking-web-server](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_blocking.png)

기존의 웹 서버들은,  
process per connection 또는 thread per connection 방식으로 동작한다.  
하나의 요청을 처리하기 위해, 전담 프로세스 또는 스레드를 생성한다.

listen socket을 통해 연결 요청을 받는 것은,  
여러 개의 listen socket을 I/O multiplexing 방식으로 non-blocking으로 수행하지만,  
실제 connection socket을 통해 요청을 처리하는 과정은 blocking으로 수행하는 것이다.

> During the time the process is run by the server, it spends most of its time ‘blocked’ – waiting for the client to complete its next move.

### NGINX의 동작 방식

![event-driven-web-server](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_nonblocking.png)

그에 반해 NGINX는 연결 전담(connection dedicated) 프로세스나 스레드를 두지 않는다.  
config에 지정된 수의 worker 프로세스만이 고정되어 있고(추천 설정은 CPU core 당 1개),  
이 worker 프로세스 들이 listen socket, connection socket 2개의 이벤트를 다 처리한다.  

### 이벤트 주도 방식이 블로킹 방식보다 빠른 이유

새로운 connection마다 프로세스 혹은 스레드를 생성한다는 것은,

- 메모리에 PCB 혹은 TCB를 생성하기 위한 공간이 필요하다
- 해당 프로세스나 스레드를 관리하기 위한 추가적인 CPU 작업이 필요하다
- 그 수가 많아질수록 Context switching이 잦아진다

공식 블로그 글에서는, 기존 웹 서버 설계에는 큰 불균형이 존재한다고 표현한다.  
HTTP connection을 처리하는 것은 가벼운 작업이지만,  
그것을 처리하기 위한 프로세스나 스레드는 무겁다는 것이다.  
이런 방식은 프로그래밍하기엔 편하지만, 효율적인 방법은 아니다.  

> However, there’s a huge imbalance: the rather lightweight HTTP connection, represented by a file descriptor and a small amount of memory, maps to a separate thread or process, a very heavyweight operating system object.

그래서, **매번 connection마다 프로세스나 스레드를 생성해주지 말자**는 것이다.  
따라서 고정된 수의 프로세스로 여러 connection을 처리하기 위해,  
이벤트가 발생할 때마다 처리해주는 방식으로 구현한 것이다.

그리고 worker 프로세스를 CPU core 수와 동일하게 생성해줌으로써,  
문맥 교환도 최소화 할 수 있다. (보통 빈도가 낮고, 해야할 일이 없을 때 발생한다.)

> 공식 블로그 글에서는, NGINX의 worker process를 체스 그랜드마스터에 비유한다.  
새로운 게임 참가자가 올 때마다, 새로운 체스 선수를 매칭시켜주는 것이 아니라,  
한 명의 체스 그랜드마스터가 돌아가면서 360명의 게임 참가자와 동시에 게임을 두는 것이다.

## NGINX 내부 구조

NGINX의 내부 구조도 빠르게 훑어보자.  

### 프로세스 모델

![nginx-process-model](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_process-model.png)

NGINX는 1개의 master process와 3종류의 자식 프로세스로 구성되어 있다.  

- master process
  - 특권 명령을 수행한다(privileged operations)
    - listen socket에 port를 바인딩
    - NGINX 설정 읽기
    - 자식 프로세스 생성 (이어지는 3가지 타입의)
- child processes
  - cache loader
    - 디스크 기반 캐시를 메모리에 불러오고, 종료됨
    - NGINX 시작 시 실행됨
    - 보수적으로 스케줄링되므로, 이 프로세스의 리소스 요구사항은 낮음
  - cache manager
    - 주기적으로 실행됨
    - 디스크 캐시를 설정된 사이즈로 유지하기 위해, 캐시 엔트리를 정리함
  - worker
    - 모든 일을 다한다!
      - 네트워크 연결을 처리
      - 디스크에 컨텐츠를 R/W
      - upstream servers와 통신

다음과 같이 확인할 수 있음

```bash
# service nginx restart
* Restarting nginx
# ps -ef --forest | grep nginx
root     32475     1  0 13:36 ?        00:00:00 nginx: master process /usr/sbin/nginx 
                                                -c /etc/nginx/nginx.conf
nginx    32476 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32477 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32479 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32480 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32481 32475  0 13:36 ?        00:00:00  _ nginx: cache manager process
nginx    32482 32475  0 13:36 ?        00:00:00  _ nginx: cache loader process
```

### worker 프로세스

NGINX의 worker 프로세스는 싱글 스레드이고, 독립적으로 실행된다.  
각 worker 프로세스들은 문맥 전환을 줄이기 위해, non-blocking 방식으로 동작한다.  

NGINX는 대부분의 경우 CPU 코어당 1개의 worker 프로세스를 실행하도록 설정하는 것을 추천한다.  
이것이 하드웨어 리소스를 가장 효율적으로 사용한다고 한다.

```bash
worker_processes auto;
```

worker 프로세스들은 다음과 같은 정보들을 공유 메모리를 통해 공유할 수 있다.

- shared cache data
- session persistence data
- other shared resources

### worker 내부 구현 살펴보기

![worker-inside](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_worker-process.png)

먼저 어떻게 worker process가 초기화되는지 살펴보자.  
worker 프로세스는 NGINX 설정에 따라 초기화되고,  
master process에 의해 listen sockets를 제공받는다.

새로운 connection 요청이 들어오면 이벤트가 발생하고,  
connection의 종류에 따라 알맞은 상태 기계에 할당된다.

- HTTP state machine
- Stream state machine
  - raw TCP
- Mail state machine
  - SMTP
  - IMAP
  - POP3

![worker-request-flow](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_request-flow.png)

각 상태 기계는, 해당 요청을 어떻게 처리해야하는지 알려주는 명령어들의 집합이라고 할 수 있다.  
NGINX 외에도 대부분의 웹 서버는 유사한 상태 기계를 통해 동일한 기능을 수행하고,  
각 웹 서버의 차이는 각 상태 기계의 구현 방법에 달려있다.

### 무중단 설정변경이나 NGINX binary 업데이트

![config-update](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_load-config-1.png)

![bianry-update](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_load-binary.png)

그림이 워낙 잘 나와있어서 이해가 쉬울 것 같다.  

설정 변경은 Blue-Green 방식과 유사하게 배포하고,  
NGINX binary 변경은 Rolling update 방식과 유사하게 배포한다.  

## 결론

결국은 다룰 수 있는 concurrent connections의 수를 증가시키기 위함이었다.  
C10k problem로 대표되는 문제는 blocking 방식의 한계였고,  
이를 해결하기 위해 event-driven architecture로, non-blocking 방식으로 해결했다.

결국은 동시에 다룰 수 있는 연결의 수가 많아져서,  
reverse proxy로서 로드밸런싱이나 다른 여러 기능들을 수행할 정도의 여력을 갖게 된 것이다.  
로드밸런싱을 하려면 애초에 많은 로드를 받아낼 수 있어야 하니까.  

NGINX 성능 튜닝과 같이, NGINX에 대해 더 깊게 공부를 하지 않아 많이 부족한 글이다.  
이는 공부하면서 내용을 추가하거나, 새로운 글을 작성하는 방식으로 개선해나가도록 하겠다 :)
