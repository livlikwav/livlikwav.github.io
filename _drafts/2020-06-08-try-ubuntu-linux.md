---
title:  "우분투 리눅스 배워보기"
excerpt: "간단하게 정리해서 남겨놓자!"


categories:
-   공부
tags:
-   인프라
last_modified_at: 2020-06-10TO22:30:00+09:00
---


# 가자가자
히히

# 정리시작

VirtualBox
GCP
AWS

먼저 VM Instance
Ubuntu

Terminal
GUI
TUI

Putty
접속

sudo 
lastb
> ip찾아보는 사이트에서 위치 찾을 수 있음

ssh localhost -l user
qwe123

클라우드에서는 ID/PW로 들어오는거 막아놓음

sshd <-- ssh demon

# Linux의 간략한 구조 

파일시스템 살펴보기

뭐가 됐건 대략적인 뼈대를 갖고 있다 
리눅스는


### 박수현님도 패캠에서 강의하신대
sshd <--ssh daemon

/etc <-- 모든 설정파일.. 웹 nignx, db, was, 기본 설정 파일

/var <-- 시스템 구동중에 필요한 변경되는 파일들 로그 pld

/home/user1
/home/hyunlove

ls -al /etc/ssh

ssh client ->
ssh server <- 접속하기.. 


sudo vi /etc/ssh/sshd/config <--sshd 설정파일 수정

/Challenge

49번째줄부터 아래로...
ChallengeResponseAuthentication no --> yes 
PasswordAuthentication no -> yes

sudo systemcti restart ssh

### 사용자 2개를 만든 이유
권한을 다르게 해서 
실험해보려고 하고 있는것

클라우드 공용 .. 팀내에서
EC2 instance keydown -> 공통 share
-> 리눅스 철학 위배하는 거다

## 나중에 프로젝트 할때 제대로 된 계정 만들고 사용하게 하는거 

password는 누구나 볼 수 있다 
shadow는 아무나 못본다

권한이 없으면 함부로 sudo라는 기능을 쓰려하면 다 기록이 남는다

시스템 관리자가 모니터링할수가 있다

## 권한이라는 것이 뭐냐

drw-r-wr-w

### 파일과 디렉토리에 대한 접급 권한
User 
Group
Other

rwx, rwx, rwx
read, write, execute(access)


-rw-rw-r-- 1 hyunlove hyunlove 0 Jun 10 10:47 hello.txt

나 hyunlove -rw 읽고쓰고
그룹 hyunlove뿐 -rw 읽고쓰고
Other -r- 읽기만 가능

## 창을 두개 만든 이유
이렇게 권한이 다른 두 사용자로 
리눅스 올바른 사용법 보여주심

## 내 파일은 권한을 마음대로 바꿀 수 있다
chmod o+w hello.txt

## 협업 과정에서

user3
hyunlove
jkim
shpark

sudo mkdir /work
### 공유 폴더로 만드는게 편하다

### sudo로 만들엇으니까 root 권한에 속해있는거 

ls -al /work

## 그래서 이제는 group을 만들어야한다 

sudo addgroup developers
### developers 라는 이름의 그룹 만든다


sudo usermod -aG developers hyunlove
sudo usermod -aG developers user1

## 그룹툴을 만들고 권한 부여하면 로그아웃했다가 다시 로그인해야한다. 

sudo chown root:developers /work
sudo chmod g+w .

## 파일마다 그룹 권한 줘야해?
chown hyunlove:developers hello.txt

# 그래서 권한은 상위 디렉토리로 부터 상속을 받아라
sudo chmod g+s

### ls -al >뭔지 찾아보기

## 여튼 저렇게 sudo chmod g+w 하면 폴더 안에 파일은 다 상속받아서 그룹 권한 받는다!


# ID PW 안좋다 > 그럼 뭐해야하냐
# KeyFile 로 접속해야한다 

window > puttygen > key를 만들수 이다 

Mac, Linux
> 본인들의 key를 terminal에서도 만들수 있다 
> 접속하고자 하는 주체에서
> 클라우드 말고

### PKI infrastructure 공개키/개인키
그 pair를 가지고 비대칭 암호화 
일반적으로 banking 할때쓰는 공인인증서
이거 다 PKI로 되어있다 
대부분의 현존 암호화 체제

공개키
개인키
### 개인키는 무조건 혼자만 알고있어야 한다

public 은 누구든지 보라고 만드는거
개인키 절대 나만

EC2 download 개인키...
### 이 개인키를 왜 친구들한테 주냐
### 소유자만, 주인만, 혼자 간직해야한다

# 좀 더 의미있고 재밌어할 시스템 서비스들에 대해서 배워보자

echo "hello"
글자 찍고 싶어

### 색깔 넣고 싶어

echo -e "\e[33mhello\e[0m"
하면 
노랑색 hello
나오고 
e31 빨강색
e32 초록색
e[32;44하면 파란색도 된다

# 시스템 명령어로 넘어가자

여러가지 서비스들이 백그라운드에서 돌고 ㅣㅆ다
### 서비스가 뭐냐
윈도우에서도 서비스라는 개념이 있다
## 윈도우 작업관리자 > 서비스 : 백그라운드에서 돌고있는 프로그램들

service --status-all
> 쓰지마세요.. deprecated
> 하위호환성때문에 유지하는거지만 
> 직믕느 안쓰는거

systemctl
> systemd 시스템 관리...

systemctl status
> 이렇게하면 서비스 쭉 보여준다
> 어마어마하게 많지?

# Systemctl으로 여러가지 서비스 다룰수 있음

systemctl status ssh
> 서비스가 돌고 있는 상태를 알 수 있다

sudo systemctl stop ssh
> 원격에 있는 ssh daemon에 대한 서비스를 중지한거기때문에 원격으로 접속이 안될 것이다

sudo systemctl start ssh
> 다시 ssh daemon 돌리는 거다


sudo systemctl enable ssh
sudo systemctl disable ssh

sudo apt install apache2 -y
> 웹페이지 다운되고 
> 뜰거 아냐 
> 웹서버 내리려면?

systemctl status apache2
> 일단 정보봐 

sudo systemctl stop apache2
> 이렇게 하면 웹서버 닫는다

curl localhost
> 이러면 failed to connect to localhost port 80: Connection refused


다시 start하면됨
### 원하는 서비스를 살리고 죽이고 할 수 있는 것이다

# 각자 프로젝트
python
java
뭐가됐건 서버를 만들었다 

보통 서버를
./start.sh
java -jar hello.jar
이런식으로 실행을 할건데

### 매번 그렇게 하려면 불편하다

## 시스템 서비스 < start/stop/enable/disable/ 헬스체크 ... 이 데몬 죽었나 살았나 죽었으면 살려줌
그래서 시스템 서비스를 만들고는 한다

# 서비스를 만들어보자가 오늘의 취지였다


cat my-service.sh
#!/bin/bash
echo "i'm in $(date +%Y%m%d-%H%M%S)" >> /tmp/mylog.log

chmod +x my-service.sh

sudo vi /lib/systemd/system/my-service.service

[Unit]
Description = My Startup

[Service]
ExecStart = /usr/local/sbin/my-script.sh

[install]
WantedBy= multi-user.target

## 지금은 실행되는 스크립트로 만들었찌 돌아가는 데몬으로 만든게 아니다
그래서 지금은 inactive로 되어 있다



cat my-service.sh
#!/bin/bash
while true
do
    echo "i'm in $(date +%Y%m%d-%H%M%S)" >> /tmp/mylog.log
    sleep 10
done

### 이렇게 하면 데몬이 맞는거임

# 버그가 생겨서 저 프로세스가 죽었다?

### 죽었다가 자동으로 띄워주는것도 스크립트에 넣어야함
그래서 지금은 PID로 죽이면 그냥 죽는다
sudo kill 16057

## 스크립트 파일로 들어와서 
[Service]
Restart=always
계속 빠르게 살리는건 더 큰 문제가 있을 수 있다
RestartSEC=5
User=user1
Group=user1
> 이렇게 다양한 옵션들을 넣을 수 있다

sudo systemct daemon-reload
>다시 돌리고 

init << SysV

Upstart (Ubuntu12) >> Systemd (Ubuntu14/16/18)

# 오늘 재밌겧 ㅏㄹ거는 아나콘다를 얼른 설치 할것이다

https://repo.anaconda.com/archive/

curl -0 https://repo.anaconda.com/archive/Anaconda3-2020.02-Lnux

bash Anaconda3<tab> -b -p /work/anaconda./anaconda/bin/coda init

source ~/.bashrc

jupyter notebook

jupyter notebook --ip=0.0.0.0 --no-browser

# 클라우드에서 개발환경을 구축하는 방법에 대한 ㅐㄴ용임

jupyter notebook password
qwe123
qwe123

jupyter notebook --generate-config
home/user1/.jupyter/jupyter_notebook_config.py

부팅에 대한 Runlevel이 있다 
CLI
Fail-mode

GUI

# 예시를 보여주는 거다 
웹서비스가 됏건 뭐가 됏건
제대로 원격지에다가 구동을해ㅓ 
돌아갈수있게할 데모다

잘되면 
도커로 컨테이너를 만들어서
그걸 배포하고 
그걸 돌리고 하는게
다른 특강의 내용들이다

오늘 맛보기 과정은 
이정도를 보여주면 
리눅스 어케하는게 제댈 쓰는거고
어떤 기능들이 있고

