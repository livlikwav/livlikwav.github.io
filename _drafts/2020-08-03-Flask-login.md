---
title:  "Flask에서 login/logout 구현하기"
excerpt: ""


categories:
-   Flask
tags:
-   flask-login
last_modified_at: 2020-08-03TO22:30:00+09:00
---

회원 가입
로그인
로그아웃
URL Mapping Controller 역할 
app.py

(html을 쓰게 되면 jinja2 렌더링 엔진 쓰겠지)

login
logout
register

[NAVER D2: 안전한 패스워드 저장](https://d2.naver.com/helloworld/318732)

### flask-base(boilerplate) 참고

from flask_login
import
    current_user
    login_required
    login_user
    logout_user

/login
GET, POST

login()
log in an existing user

form = loginform()
if form.validate_on_submit():

### flask MVC 패턴 회원가입 기능 만들기

그냥 flask.request 에서 가져옴 properties 에서

### 쿠키와 세션

Cookie
Session
클라이언트와 서버가 정보르 주고받는 쿠키와 세션

쿠키
> 시간이 지나면 소멸하고
> 서버의 자원을 활용하지 않고
> 클라이언트 쪽에 저장된다
그래서 로그인 같은 보안기능을 활용할 때는 세션을 활용

플라스크에서는 세션을 
딕셔너리 형태로 제공한다

세션과
회원가입때 받아두었던 DB의 id 필드, password 필드와 일치하는지 확인하면서 
로그인 기능을 구현한다

로그아웃은
세션을 제거하면 끝

### 쿠키와 세션

사용하는 이유
HTTP 프로토콜의 특징이자 약점을 보완하기 위해서 사용한다

HTTP protocol features

- Connectionless
- Stateless

Stateless 무상태성
> 연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며
> 상태 정보는 유지하지 않는 특성이 있다.

무상태성을 보와나기 위해서 쿠키와 세션을 사용한다.
통신할 때마다 새로 커넥션을 열기 떄문에
클라이언트는 내가 누구인지 인증을 계속해야하는 단점이 생긴다.

쿠키와 세션이 없다면
어떤 페이지에서 옮겨다닐때마다 로그인을 다시해야한다

### 쿠키

쿠키는,
클라이언트 로컬에 저장되는,
Key:Value 가 들어있는 작은 데이터 파일이다.

쿠키에는,
이름, 값, 만료날짜(쿠키 저장기간), 경로 정보가 들어있다.
일정시간동안 데이터를 저장할 수 있다.

쿠키프로세스

1. 브라우저에서 웹페이지 접속
2. 클라이언트가 요청한 웹페이지를 받으면서 쿠키를 클라이언트 로컬(하드)에 저장
3. 클라이언트 재 요청시 웹페이지 요청과 함께 쿠키값도 전송
4. 지속적으로 로그인 정보를 가지고 있는 것처럼 사용

사용 사례

- 자동 로그인
- 오늘 더 이상 이 창을 보지 않음 체크
- 쇼핑몰의 장바구니

쿠키의 제한

- 300개 까지 쿠키 저장 가능
- 한 도메인당 20개의 값만 가질 수 있음

브라우저가 Request시에 Request Header에 넣어서 자동으로 서버에 전송
Response Header에 Set-cookie 속성을 사용하면 클라이언트에 쿠키를 만들 수 있다.

### 세션

일정시간 동안 같은 브라우저로 부터 들어오는 일련의 요구를
하나의 상태로 보고 그 상태를 유지하는 기술

즉, 웹 브라우저를 통해 웹 서버에 접속한 이후로
브라우저를 종료할 때 까지 유지되는 상태

클라이언트가 Request를 보내면,
해당 서버의 엔진이,
클라이언트에게 유일한 ID를 부여하는데 이것이 세션ID다.

### 세션 프로세스

1. 클라이언트가 서버에 접속시 세션 ID를 발급
2. 서버에서는 클라이언트로 발급해준 세션 ID를 쿠키를 사용해 저장
3. 클라이언트는 다시 접속할 때, 이 쿠키를 이용해서 세션ID값을 서버에 전달

즉 세션을 구별하기 위해 세션 ID가 필요하고,
그 ID만 쿠키를 이용해 저장해 놓는다
쿠키는 자동으로 서버에 전송되니까 서버에서 세션아이디에 따른 처리를 할 수 있음.

예를 들면 게시판에 글을 작성할 때,
작성 버튼을 누르면
세션에 있는 아이디를 참조해서 작성자를 지정하게 한다.

세션 사용 사례
로그인 정보 유지

### 쿠키와 세션의 차이

1. 저장 위치
   1. 쿠키 클라이언트 파일
   2. 세션 서버
2. 보안
   1. 쿠키는 클라이언트 로컬에 저장되기 때문에 변질되거나 request에서 snipping 가능
   2. 세션은 쿠키를 이용해서 sessionid만 저장하고
   3. 그것으로 구분해서 서버에서 처리하기 때문에 비교적 보안성이 좋다

세션은 ㅁ브라우저가 종료되면
만료시간에 상관없이 삭제된다.

### Authentication & Authorization

Authentication 이 인증
Authorization 이 인가

인증을 위해서 bcrypt 알고리즘을 사용하여 
회원의 패스워드를 단방향 암호화함

### 회원가입 API with bcrypt

sign-up 엔드포인트 부분에서
password 부분을 bcrypt 알고리즘과
hashpw 함수를 넣어 수정한다

### 인증

아이디와 비밀번호를 확인하는 절차
User's identification 확인하는 절차
인증 하기전에 아이디와 비밀번호 생성을 해야겠지.

### 로그인 절차

1. 유저 회원가입 > 비밀번호 암호화 저장
2. 비밀번호 암호화해서 DB 저장
3. 유저 로그인 > 아이디와 비밀번호 입력
4. 유저가 입력한 비밀번호를 암호화한 후, DB에서 암호화된 비밀번호와 비교
5. 일치하면 성공
6. 로그인 성공하면 access_token 을 클라이언트에게 전송
7. 로그인 성공후 다음부터는 access_token을 첨부해서 request를 서버에 전송

### Bcrypt

`bcrypt.hashpw(b"secrete password", bcrypt.gensalt())`
`bcrypt.hashpw(b"secrete password", bcrypt.gensalt()).hex()`

### JWT = JSON Web Token

유저 로그인
POST /auth HTTP/1.1
HOST: localhost:5000
Content-Type: application/json
{
    "username":"joe",
    "password":"pass"
}

이렇게 보내면

HTTP/1.1 200 OK
Content-Type: application/json
{
    "access_token" : "asdadasdarwerwjefowkfoskdpofkwopekfw"
}

이런식으로 access_token을 request 메세지에 넣어 서버에 보낸다

## 인가 Authorization

유저가 요청하는 request를 실행할 수 있는 권한이 있는 유저인가를 확인
(해당 유저는 고객 정보를 볼 수 있지만 수정할 권한이 없는 경우)

Authorizationeh JWT를 통해서 구현이 가능하다

### 인가 절차

1. access_token 을 생성한다. access_token에는 유저 정보를 확인가능 정보가 들어가 있어야한다
2. request에 access_token 첨부해서 보낸다
3. 서버는 access_token 복호화
4. 거기서 user id 얻어
5. user id 통해서 유저의 권한 확인해
6. 충분한 권한 가지고 있으면 처리함
7. 아니면 401 혹은 다른 에러 코드 보냄

## Naver D2 안전한 패스워드 저장

패스워드를 저장할 때 해시 함수를 사용한다
대부분의 웹 사이트에서 사용하고 있는 암호화 알고리즘의 안정성을 검토한다
어떤 암호화 알고리즘을 사용해야 안전한지 설명한다

단방향 해시 함수
두가지중 한가지로 보통 패스워드 저장한다

1. 단순 텍스트 plain text
2. 단방향 해시 함수 one-way hash func 의 다이제스트 digest

단순 텍스트로 저장하면 범죄를 저지르는 것이나 다름없다

암호화된 메시지 = 다이제스트

원본 평문과 전혀 달라지게 하는 효과 = avalanche 효과

### 단방향 해시 함수의 문제점

SHA-256같은 해시 함수 사용해
패스워드를 암호화해 저장하고 값을 비교하는 것만으로 충분하다고 생각하는데
2가지 문제점이 있다

1. 인식 가능성 recognizaability

동일한 메시지가 언제나 동일한 다이제스트를 갖는다면?

공격자가 pre-computing된 digest > save as big as possible
찾아내 brute-force로

다이제스트 목록  = rainbow table
rainbow attack = 이러한 공격 방식

2. 속도 speed

해시는 원래 패스워드를 저장하기 위해서 설계된 것이 아님.
짧은 시간에 데이터를 검색하기 위해 설계됨.
그래서 빨리 털 수 있음

### 단방향 해시 함수 보완하기

1. 솔팅 salting

솔트 = salt
단방향 해시 함수에서 다이제스트를 생성할 때 추가되는 바이트 단위의 임의의 문자열이다.

솔팅 salting
원본 메시지에 문자열을 추가하여 다이제스트를 생성하는 것

솔팅된 다이제스트를 대상으로 패스워드 일치 여부를 확인학 ㅣ어렵다

사용자 별로 다른 솔트를 사용한다면,
동일한 패스워드를 사용하는 두 사용자라도
다이제스트가 다르게 생성된다.

솔트와 패스워드의 다이제스트를 DB에 저장
사용자 로그인시 패스워드를 해시함
모든 패스워드가 고유의 솔트를 갖고
솔트의 길이는 32바이트 이상

2. 키 스트레칭 key stretching

해시를 반복함

하나의 다이제스트 생성할 때 어느 정도의 시간 소요되게 한다

자신만의 암호화 시스템을 구현하는 것은 매우 위험하다.
취약점을 확인하기 어렵다.
점검하고 확인하는 사람은 한명이다.

예시중에 bcrypt가 있다.
애초에 패스워드 저장을 목적으로 설계됨.

key derivation function 중에 bcrypt도 있는 것이다.

최대한 긴 패스워드를 사용하도록 권장해야한다.

### 로그인 API with bcrypt

사전에 회원가입 한 유저들이 요청하는 응답하는 엔드포인트
회원가입시 보냈던 유저의 email과 pw를 받고
DB에 저장되어 있는지
저장된 값과 일치하는 지 확인한다
인가되는 부분에서 활용할 JWT를 응답하여 준다

POST로 요청받아야함
uri에 나오면 안대자너

`bcrypt.checkpw(password.encode('UTF-8'), row['hashed_password'].encode('UTF-8'))`

