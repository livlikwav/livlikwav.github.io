---
title:  "GitLab 사용기"
excerpt: "Github과 다른점은? CI/CD 툴으로써의 깃랩?"


categories:
-   CI/CD
tags:
-   Gitlab   
last_modified_at: 2020-07-18TO22:30:00+09:00
---

### add SSH key

처음 project에 들어가니까, 상단 알림으로 SSH key를 설치하라고 나온다.

different types of SSH key
gitlab supports ...

- RSA
- DSA
- ECDSA
- ED25519

difference lies on the signing algorithm
we'll focus on ED25519 and RSA

[Using Ed25519 for OpenSSH keys instead of DSA, RSA, ECDSA](https://linux-audit.com/using-ed25519-openssh-keys-instead-of-dsa-rsa-ecdsa/)
이런 글까지 있는거 보면 그냥 ED25519 바로 쓰자.

they are more secure and better performance

### Generating a new SSH key pair

1. open zsh
2. generate a new ED25519 SSH key pair
   1. use suggested path = dont need additional config
3. input a password to secure new SSH key pair

### deploy keys
[참고 링크](https://blog.leocat.kr/notes/2017/11/27/github-deploy-key)
배포서버에서 gitlab으로 commit 한다거나 pull 받아야 할 때,
특정 사용자로 로그인하기 애매할 때, 로그인 안하고 ssh를 통해 로그인 하지 않고 접근하기 위함

### adding an SSH key to Gitlab account

copy public key, and paste it in gitlab SSH key

### Testing that everything is set up correctly

## Auto DevOps

provides pre-defined CI/CD config
allow you to automatically detect, build, test, deploy, and monitor apps
simplify the setup and execution of a mature & modern sw development cycle

pipeline
Job묶음

Job은 다음과 같다

- 테스트
- 린트
- 빌드
- 배포

## 온프레미스 On-premise

- 전통적인
- 솔루션을 자체적으로 보유한 전산실 서버에 직접 설치해 운영하는 방식
- 클라우드 같이 원격 환경이 아님
- 클라우드 나오기 전의 기업 인프라 구축의 일반적인 방식
- 보안적인 이유로 비즈니스에 중요하고 보안이 필요한 서비스와 데이터는 온프레미스로 하고
- 덜 중요한 것은 퍼블릭 클라우드를 사용하는
- 하이브리드 IT 인프라가 대세이다

