﻿---
title:  "Node js 사용기"
excerpt: "Node js가 무엇이고, Node js를 선택하게 된 이유를 정리합니다."

categories:
  - Job Interview
tags:
  - Job Interview
last_modified_at: 2020-05-05TO23:30:00+09:00
---

# 위키피디아 : Node.js
[https://ko.wikipedia.org/wiki/Node.js](https://ko.wikipedia.org/wiki/Node.js)
![Node.js logo.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/220px-Node.js_logo.svg.png)
**Node.js**는 
- 확장성 있는 네트워크 애플리케이션(특히 서버 사이드) 개발에 사용되는 
- 소프트웨어 플랫폼이다. 
- 작성 언어로  자바스크립트를 활용하며 
- **Non-blocking I/O**와 
- **단일 스레드 이벤트 루프**를 통한 
- **높은 처리 성능**을 가지고 있다.

- **내장 HTTP 서버 라이브러리**를 포함하고 있어
- 웹 서버에서 아파치 등의 별도의 소프트웨어 없이 동작하는 것이 가능하며 
- 이를 통해 웹 서버의 동작에 있어 더 많은 통제를 가능케 한다.

### Node.js 공식 소개 문서
[https://nodejs.org/ko/about/](https://nodejs.org/ko/about/)

# NODE JS - node js , express.js 란?  
출처: [https://dydals5678.tistory.com/88](https://dydals5678.tistory.com/88) [아빠개발자의 노트]
### NODE JS 란?
- back-end (서버기술) 로
- 프론트가 아닌 백엔드에서도 javascript기술을 쓸수 있게 고안된 언어.
- NPM : Node Package Manager
### Express.js 란?
- Node.js 의 프레임워크다
- java 의 스프링, php 의 라라벨, 파이썬의 django 같은 프레임워크다.
- express.js 의 경우 github의 마지막 커밋이 2달전 4년전 1년전이다.
- 그만큼 준비가 다되있고 완벽,완성에 가까운 프레임 워크라는거다.
- 가장 많이 쓰이는 프레임워크다.

# 블로그 : Node JS 장단점을 개인적으로 느낀 부분 과 싱글스레드에 대하여
[https://epdl-studio.tistory.com/76](https://epdl-studio.tistory.com/76)
Node Js는 
- Chrome V8 JS 엔진으로 빌드된 JavaScript 런타임입니다
- 이벤트 기반
- 논 블로킹 IO 모델을 사용해 
- 가볍고 효율적이다.
Node js 의 **패키지 생태계인 npm**은 
- **세계에서 가장 큰 오픈 소스 라이브러리 생태계**이기도 하다.

### 필자가 느낀 부분
프론트 엔드 개발자도 쉽게 백엔드 서버를 약간의 공부로 구현할 수 있고, 백엔드 개발자도 node js를 공부하면 자바스크립트와 프론트 단을 쉽게 이해할 수 있다라는 점이다.

### Node JS 장점
1. V8 engine 위에서 작동하는 이벤트 처리 I/O 프레임 워크이다.
> 크롬의 엔진인 V8의 경우 구글이 꾸준히 업데이트하고 개발을 하고 있어서 앞으로도 성능이 좋아질 것 이다
2. 이벤트 처리 방식(Evnet-Driven)으로 비동기 프로그래밍이다.
> 비동기라는 점은 결과값을 바로 받지 않기 때문에 다양한 요청(이벤트)을 받을 수 있고 빠른 속도를 자랑할 수 있다.<br>
2-1 CPU 대기 시간을 최소화 할 수 있다.<br>
2-2 CPU 부하가 적고 많은 커넥션을 동시에 처리할 수 있다.(넷플릭스, 페이스북)
3. 프론트 엔드와 백엔드를 자바스크립트 같은 언어로 만들 수 있다.
> 프론트와 백엔드 언어가 비슷하기 때문에<br>
>  쉽고 빠르게 공부할 수 있고 빠르게 결과물은 만들 수 있다.<br>
>  그래서 성능이 좀 떨어지더라도 생산성을 어마어마하게 크다는 점이다.

### Node JS 단점
~~1. 싱글 스레드 이기 때문에 하나의 작업이 오래 걸리면 시스템 전체의 성능이 떨어진다.~~(이해가 안되서 넘겼음)
2. 이벤트 콜백 중심으로 코드가 중첩이 되는데, 가독성과 유지보수가 힘들다.
3. 에러가 발생하면 프로세스 자체가 죽어버린다.

자바로 만든 웹서버는
- 웹서버는 관리하기도 좋고 생산성도 좋다
- 멀티 스레드로 개발을 정말 잘해야 성능이 좋다
- 하지만 많은 자바 개발자들이 멀티 스레드 개발을 제대로 못해 성능저하가 일어난다.
- 그래서 CPU에 멀티스레드를 나눠놓아도 CPU에는 많은 간섭이 있다.

Node JS 싱글스레드의 경우에는 
- CPU 부하가 많이 적고 별다른 간섭이 적어서
- 훌륭한 퍼포먼스가 나온다라는 점이다.
- 그래서 약간의 공부를 통해서 개발을 쉽게 
- 어지간한 퍼포먼스가 나오는 REST API 서버를 만들 수 있다.

# 블로그 : [이메일 문답] Angular + Node.js vs. Spring  
출처: [https://han41858.tistory.com/41](https://han41858.tistory.com/41) [한장현입니다.]

질문 : 
- 백엔드를 node js 로 구성하고 프론트를 Angular로 구성하려 한다
- 스프링에도 백엔드 프론트엔드 모두 있다고 한다.
- 두 프레임워크에 대한 장단점을 파악하기가 저로서는 난감한 상황이다.
- 추구하고자 하는 것은 
- 앞으로 발전가능성이 크면서 
- 중간정도 프로젝트 규모에서 안정적으로 잘 돌아가는 환경 
- 시간투자대비 생산성에 중점을 두려고 한다

답변
Spring은
- Spring은 Java 백엔드 프레임워크
- 오래 사용된 것이기 때문에
- 알려진 버그와 보안 문제는 많이 잡혀있고
- 안정성이 우수하다.
- 정형화되어있는 패턴이 있고 
- 막혔을때 다른 사람에게 물어보기 쉽다
- 대기업이나 정부과제에 많이 사용한다
- Dl 이나 IoC에 대한 개념도 충실히 들어있다


Node.js는
- JS 백엔드 프레임워크이며
- 운영환경이기도 하지만 이 논의에서는 프레임워크로만 생각 
- 가장 좋은 점은 
- 모든 개발 스택에서 JavaScript를 사용할 수 있다는 것인데
- 백엔드부터 프론트엔드까지, 더 확장하면 DB도 JS로 구현할 수 있다
- 아주 간단한 서버는 코드 10줄 정도로 구현할 수 있다

Angular는
- 프론트엔드 프레임워크이며
- 프론트엔드 SPA를 만들수있는 기능을 다양하게 제공한다
- Angular는 온전히 프론트엔드의 영역이므로 이 논의에서 제외

**Spring에 백엔드와 프론트엔드가 같이 있다는 말은**
- 서버의 입장에서 프론트엔드 코드를 보내는 백엔드가 있다는 것을 혼동하신 것 같다.
- 그렇다고 해서 **Spring 프레임워크가 프론트엔드에 적극적으로 개입하는 것은 아니며,**
- **JSP와 서블릿 사용해서 프론트엔드 개발하는 것은 조금 다른 문제**이다.
- Spring은 어디까지나 서버 프레임워크이다.

웹 표준에서 
- HTML문서는 DOM 마크업과 JS, CSS로 이루어지며,
- JSP와 서블릿을 사용한다면 HTML을 JSP로 컨트롤 할 수 있지만,
- 이 부분은 JS의 역할을 일부 가져온 것일 뿐이다.

**그렇게 보면 가장 큰 차이는 Java나 JS냐의 차이이며**
- 최신 트렌드를 얼마나 반영할 수 있느냐,
- 안정적이냐,
- 자유도는 얼마나 있느냐의 문제이다.

비교 
- **Spring은** **정형화된 패턴 위주로 개발**하며
- 자유도는 낮지만 
- 같은 이유로 안정성은 높다

- **Node js는** **딱 정해진 패턴은 없으며**,
- **npm에 있는 모듈을 활용할 수 있고**
- JS 특성상 자유롭게 개발할 수 있다.

> MVC모델과 이벤트 드리븐의 차이도 있지만, MVC모델에서 HTTP 요청이 들어왔을 때 어떤 로직을 처리한다고 보면 이벤트 드리븐이라고 봐도 크게 다르지 않다.

**결국엔 개발언어의 차이인 것 같다.**
- Spring을 사용하는 경우에는
- Java 외에 프론트엔드에 JS도 사용해야 하며 
- DB가 SQL이든 NoSQL이든 
- 이부분도 Java외에 다른 언어를 사용해야 한다.

**개발 언어 외에, 처리하는 데이터 객체도 각 스택마다 다르다**
- SQL로 가져온 데이터는 
- Java에서 데이터 오브젝트(DO)로 처리하고 
- 프론트엔드에서는 JSON으로 처리한다

- **Node js를 JSON NoSQL과 함께 사용하는 경우**
- **모든 스택이 JS를 사용한다**
- DB에서 **JSON 객체**를 가져와서 백엔드에서 **JSON**으로 처리하고 
- 프론트엔드에서도 **JSON**으로 처리한다
- Node js 개발 스택 중 가장 인기 있는 **MEAN 스택**은 이것이 가장 큰 장점일 것이다.

보통 Spring은 **엔터프라이즈급 프로젝트에 적합**하다고 하고,<br>
Nodejs는 **빠르게 개발하는 프로젝트나 프로토타입에 적합**하다고 생각한다.<br>
**시간투자대비 생산성** 측면에서는 잘 아는 언어와 프레임워크를 사용하는 것이 당연히 좋다.
- Spring : 어떻게 개발해야하는지 막혔을때 찾아보기 쉬운것
- Node js : 적은 양의 코딩으로 빠르게 개발할 수 있는 것

# 블로그 : Node.js vs Java 구조적 차이 :: 마이구미  
출처: [https://mygumi.tistory.com/154](https://mygumi.tistory.com/154) [마이구미의 HelloWorld]
- **[Node.js Architecture - Single Threaded Event Loop](http://www.journaldev.com/7462/node-js-architecture-single-threaded-event-loop)** 링크를 참고하여 작성된 글이다.  
- 정확히는 멀티 스레드(Multithreaded) 구조와 싱글 스레드 이벤트 루프(Single Threaded Event Loop) 구조의 차이점이 이번 글의 주제가 된다.  
- HTTP 요청/응답에 대한 내부를 알아볼 것이다
- 이해를 돕기 위해 구조로써, Spring + JSP 와 Node.js를 비교한다.

![멀티 스레드](https://t1.daumcdn.net/cfile/tistory/222A623A5905B6CE2B)
> 멀티 스레드 기반의 HTTP 요청/응답 모델 예시 그림 (Spring + JSP) 

![싱글 스레드 이벤트 루프](https://t1.daumcdn.net/cfile/tistory/2359A5425905F7B008)
> Node.js의 싱글 스레드 기반의 구조 예시그림

**싱글 스레드 이벤트 루프 방식의 장점**은 아래와 같다.
-   점점 더 많은 동시에 발생하는 클라이언트의 요청을 처리하는 것이 쉽다.
-   동시에 발생하는 클라이언트의 요청이 증가할 때, 이벤트 루프를 이용하기 때문에 많은  스레드를 이용하지 않는다.
-   멀티 스레드 방식보다 스레드를 덜 이용하기 때문에 메모리 또는 자원 소모가 작다.

이벤트 루프를 코드로 나타내면 아래와 같다.
```
public class EventLoop {
  while(true){
    if(Event Queue receives a JavaScript Function Call){
      ClientRequest request = EventQueue.getClientRequest();
      If(request requires BlokingIO or takes more computation time)
        Assign request to Thread T1
      Else
        Process and Prepare response
    }
  }
} 
```

# 위키피디아 : 솔루션 스택
[https://ko.wikipedia.org/wiki/%EC%86%94%EB%A3%A8%EC%85%98_%EC%8A%A4%ED%83%9D](https://ko.wikipedia.org/wiki/%EC%86%94%EB%A3%A8%EC%85%98_%EC%8A%A4%ED%83%9D)

솔루션 스택(solution stack)은
- 소프트웨어 스택(software stack)와 같은말.
- 애플리케이션 지원에 추가 소프트웨어가 필요하지 않는
- 완전한 플랫폼을 만드는데
- 필수적인 소프트웨어 하위 시스템 
- 또는 구성 요소들의 모임이다
> 애플리케이션은 이렇게 만들어진 플랫폼 "위에서 실행된다"로 이야기한다.

이를테면,<br> 
**웹 애플리케이션을 개발**하기 위해 설계자는 
- 대상 운영 체제
- 웹 서버
- 데이터베이스
- 프로그래밍 언어으로
스택을 정의한다. 

다른 버전의 소프트웨어 스택은 
- 운영 체제
- 미들웨어
- 데이터베이스
- 애플리케이션이다.
> 일반적으로 소프트웨어 스택의 구성 요소들은 개별 개발자들에 의해 다른 개발자와는 독립적으로 개발된다.

> "솔루션 스택"이라는 용어는 역사적으로 전체 솔루션의 일부로서 하드웨어 부품들을 포함했으며, 지원 계층에서 하드웨어와 소프트웨어가 둘 다 혼재되어 있다.

### 예시 
MEAN[10]
- 몽고DB (데이터베이스)
- Express.js (앱 컨트롤러 서버)
- AngularJS (웹 앱 애플리케이션)
- Node.js (웹 서버)
MERN[17]
- 몽고DB (데이터베이스)
- Express.js (앱 컨트롤러 서버)
- 리액트 (자바스크립트 라이브러리) (웹 앱 애플리케이션)
- Node.js (웹 서버)
MEVN[18]
- 몽고DB (데이터베이스)
- Express.js (앱 컨트롤러 서버)
- Vue.js (웹 앱 애플리케이션)
- Node.js (웹 서버)
NMP[19]
- Nginx (웹 서버)
- MySQL 또는 MariaDB (데이터베이스)
- PHP (프로그래밍 언어)

# 위키피디아 : MEAN
[https://ko.wikipedia.org/wiki/MEAN](https://ko.wikipedia.org/wiki/MEAN)
MEAN은 동적 웹 사이트와 웹 애플리케이션을 개발하기 위한 자유-오픈 소스 자바스크립트 소프트웨어 스택이다.[1]

MEAN 스택은 몽고DB, Express.js, AngularJS (또는 Angular), Node.js이다. MEAN 스택의 모든 구성 요소들이 자바스크립트로 작성된 프로그램들을 지원하기 때문에 MEAN 애플리케이션들은 서버 사이드와 클라이언트 사이드 실행 환경을 위해 오직 하나의 언어로 작성이 가능하다.

MEAN 스택의 구성 요소는 다음과 같다:[2][4]

MongoDB: NoSQL 데이터베이스
Express.js: Node.js에서 실행되는 웹 프레임워크
Angular.js 또는 Angular: 브라우저 자바스크립트 엔진에서 실행되는 자바스크립트 MVC 프레임워크
Node.js: 이벤트 드리븐 서버 사이드 및 네트워크 애플리케이션을 위한 실행 환경

# 그외 이해에 도움이 되는 글들
## 참고 블로그 : JS 자바스크립트 런타임이란?
[https://beomy.github.io/tech/javascript/javascript-runtime/](https://beomy.github.io/tech/javascript/javascript-runtime/)
런타임이란
- **프로그래밍 언어가 구동되는 환경**을 말한다.
- 위키 링크에서 런타임 환경을 일컫음
Node.js나<br>
크롬등의 여러 브라우저들은 
- **자바스크립트가 구동되는 환경**이기 때문에,
- Node.js나 브라우저들을 자바스크립트 런타임이라고 합니다.

### 싱글스레드, 논 블로킹 언어 : JavaScript
자바스크립트는 싱글 스레드, 논 블로킹 언어입니다.
**싱글 스레드**<br>
- 싱글 스레드는 **하나의 힙 영역과 하나의 콜 스텍**을 가집니다. 
- 하나의 콜 스택을 가진다는 의미는 
- 한 번에 한 가지 일 밖에 하지 못한다는 의미입니다.
- 예를 들어 네트워크 요청을 한다면 
- 응답이 올 때까지 다른 일은 하지 못하고 마냥 기다릴 수 밖에 없다.
**콜 스택**<br>
- 콜 스택은 함수가 실행되는 순서를 기억하고 있습니다.
- 함수를 실행하려면 
- 스택의 가장 위에 해당 함수를 넣게 되고,
- 함수에서 리턴이 일어나면 
- 스택의 가장 위쪽에서 함수를 꺼냅니다.
**블로킹 상태의 문제점**
- 웹 브라우저에서 코드가 실행되는데,
- 코드가 종료될 때까지 유저가 클릭을 해도 
- 어떠한 반응을 하지 않는 상태가 된다.
- 콜 스택이 멈춘 상태를 블로킹 상태라고 한다.
**블로킹 상태를 해결하는 방법이 논-블로킹, 비동기 콜백을 사용하는 것이다**<br>
- 예를 들어 5초 후 호출되는 비동기 콜백으로 블로킹 문제를 해결할 수 있다.
**자바스크립트 런타임은**
- 자바스크립트 엔진 
- Web API
- 콜백 큐
- 이벤트 루프 
- 렌더 큐
- 로 구성됩니다.
- setTimeout이나 ajax(HTTP 요청), DOM 이벤트 등의 메서드는 자바스크립트 엔진에 정의되어 있지 않습니다.
- 이러한 메소드는 Web API가 지원합니다.
- 이러한 메소드들은 콜백으로 비동기 동작을 합니다.


## 위키피디아 : 런타임이란
[https://ko.wikipedia.org/wiki/%EB%9F%B0%ED%83%80%EC%9E%84](https://ko.wikipedia.org/wiki/%EB%9F%B0%ED%83%80%EC%9E%84)
**런타임은**
- 컴퓨터 과학에서 컴퓨터 프로그램이 실행되고 있는 동안의 동작을 말한다
**런타임이라는 용어는**
- 컴퓨터 언어 안에 쓰인 프로그램을 관리하기 위해
- 특정한 컴파일러나 가상 머신이 사용하는 
- 기본 코드의 라이브러리나 프로그램을 가리키는 
- 런타임 라이브러리라고도 일컫는다.
**런타임 환경 (Runtime Environment)는**
- 컴퓨터가 실행되는 동안 프로세스나 프로그램을 위한
- SW 서비스를 제공하는 가상 머신의 상태이다.
- OS 자체에 속하는 경우도 있고
- OS에서 작동하는 SW를 뜻할 수도 있다.
**저명한 런타임**
- JVM 자바 가상머신 
- V8
	- node.js
- PyPy
- ART 안드로이드 런타임