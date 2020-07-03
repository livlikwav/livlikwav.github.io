---
title:  "터린이 맥린이의 맥북 개발환경 세팅기"
excerpt: "이제 카페에서 터미널 키고 콤퓨타 잘하는 척할 수 있는걸까요?"


categories:
-   툴
tags:
-   macOS
last_modified_at: 2020-07-03TO22:30:00+09:00
---

- [일단 맥을 샀더니 뭔가 알아야할 것들이 많아졌다](#일단-맥을-샀더니-뭔가-알아야할-것들이-많아졌다)
  - [맥북 기본 설정](#맥북-기본-설정)
  - [macOS APP](#macos-app)
  - [기타](#기타)
- [개발 환경 설정](#개발-환경-설정)
  - [참고한 글](#참고한-글)
  - [vi 에디터는 또 뭐야](#vi-에디터는-또-뭐야)
  - [vi 말고 vscode로 바로 열어서 수정할래](#vi-말고-vscode로-바로-열어서-수정할래)
  - [코딩 폰트의 중요성](#코딩-폰트의-중요성)

## 일단 맥을 샀더니 뭔가 알아야할 것들이 많아졌다

사실 그냥 보고만 있어도 좋긴하다. 이쁘니까.

요즘 내게 '생산성'이라는 키워드는 계속 머리 속에 맴돈다.
JYP는 시간이 아까워서 한 계절에 2벌의 옷만 입고, 운동화도 로우만 신는다더라.

조금이라도 놀고, 멍때리고, 운동할 시간을 벌기 위해서
치열한 생산성 향상을 통해 티끌 같은 시간들을 모아야 하는 것이다.

다들 맥을 사면 이야기하는 큰 장점인 터미널부터 시작해서,
여러 편리한 설정과 기능들을 블로그를 전전하면서 세팅해봤다.

### 맥북 기본 설정

- 트랙패드
  - 터치 클릭
  - 세 손가락 드래그
- 키보드
  - 단축키 설정
    - 이메일 주소

### macOS APP

- Magnet
  - 윈도우 노트북에서 쓰다가 맥에는 없어서 불편했다.
  - 돈이 아깝지 않다.
- iStat
  - 내 소중한 맥북이가 잘 돌아가고 있는건지 너무 궁금했다
  - 확인한다고 해서 달라지는건 없지만 마음이 든든하다

### 기타

- 크롬
  - 검색 엔진 단축키 설정
    - g: google, n: naver 등등

## 개발 환경 설정

설치한 것들 ...

- Homebrew
- iTerm2
- iTerm Color Theme
  - Snazzy
- iTerm Fonts
  - D2Coding
- 터미널에 사용자 이름 삭제
- new line 명령어
- zsh-syntax-highlighting
- fzf

### 참고한 글

[macOS 개발환경 세팅 참고 글 링크 1](https://subicura.com/2017/11/22/mac-os-development-environment-setup.html)
[macOS 개발환경 세팅 참고 글 링크 2](https://medium.com/harrythegreat/oh-my-zsh-iterm2%EB%A1%9C-%ED%84%B0%EB%AF%B8%EB%84%90%EC%9D%84-%EB%8D%94-%EA%B0%95%EB%A0%A5%ED%95%98%EA%B2%8C-a105f2c01bec)
[macOS 개발환경 세팅 참고 글 링크 3](https://ooeunz.tistory.com/21)
[FZF 세팅](https://medium.com/harrythegreat/fzf%EB%A1%9C-zsh-%ED%84%B0%EB%AF%B8%EB%84%90-%EB%8D%94-%EA%B0%95%EB%A0%A5%ED%95%98%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-730c20eb496b)

- iTerm2
  - 맥의 터미널 보조 프로그램
- Homebrew(brew)
  - 맥에서 라이브러리나 플러그인등을 쉽게 설치하게 도와주는 패키징 매니저
- ZSH
  - 쉘의 확장판
- Oh My ZSH
  - ZSH를 더 쉽게 사용해주는 플러그인
  - 설치했는데 긴 오류가 뜬다면? [참고링크](https://goax.tistory.com/4)

### vi 에디터는 또 뭐야

사실 git bash에서 commit 할 때마다 고통받긴 했었다.
gitkraken 사용하게 되면서 맘 편했는데,
이젠 피할 수 없다!!

[vi 명령어 참고 링크](https://blockdmask.tistory.com/25)

### vi 말고 vscode로 바로 열어서 수정할래

[vscode --> code 명령어 넣기 참고 링크](https://velog.io/@nmy0502/Mac-OS-%ED%84%B0%EB%AF%B8%EB%84%90terminal-%EC%84%A4%EC%A0%95)
code 원하는파일 --> 하면 vscode 실행하면서 바로 수정 가능하다.

### 코딩 폰트의 중요성

[해당 글 링크](https://ppss.kr/archives/66633)
좋은 글이 있어서 저장해두기.
