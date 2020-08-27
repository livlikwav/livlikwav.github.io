---
title:  "VIM 학습일지, 멋을 향한 여정"
excerpt: "스벅 딱 가서, 터미널 열어서 git이고 vim이고 그냥 다 ..."


categories:
-  Tools
tags:
-  Vim
last_modified_at: 2020-08-22TO20:30:00+09:00
---
- [Vim 공부 시작](#vim-공부-시작)
  - [참고한 글](#참고한-글)
  - [Vim의 장점](#vim의-장점)
  - [Vim 학습계획](#vim-학습계획)
  - [Vim을 배우기 위한 도구들](#vim을-배우기-위한-도구들)
- [Vim 학습 일지](#vim-학습-일지)
  - [1주차](#1주차)
- [중도 포기 후 근황](#중도-포기-후-근황)
  - [1. Backend REST API 개발](#1-backend-rest-api-개발)
  - [2. Git CLI](#2-git-cli)
  - [3. Dotfiles repo와 Shell script](#3-dotfiles-repo와-shell-script)

## Vim 공부 시작

### 참고한 글

[[번역] Vim 정복하기: 4주 계획](https://medium.com/@jungseobshin/vim-%EB%B0%B0%EC%9A%B0%EB%8A%94-%EB%B2%95-4%EC%A3%BC-%EA%B3%84%ED%9A%8D-77f3f7e263f7)
[완전 초보를 위한 Vim](https://nolboo.kim/blog/2016/11/15/vim-for-beginner/)

### Vim의 장점

1. Unix 기반 시스템에 기본으로 설치되어 있다.
   1. MacOS에는 물론 설치되어 있다.
   2. **서버 환경에서 바로 실행하여 파일 수정가능하다는 것이 장점**
2. 다른 에디터들과 비교하여 매우 가볍다
3. 키보드 중심으로 동작하기 때문에 **트랙패드 까지도 손이 안가도 된다.**

무엇보다... **멋있다.**
능숙하게 다루는 것만으로, 아 저사람 욕심 좀 있구나 하는 느낌이다.

### Vim 학습계획

첫번째 글의 4주 계획을 따라가본다.
매일매일 일지로 남긴다.
Vim 배우기 4주 계획은 다음과 같았다.

1. vimtutor 하루에 한 번, 매일 끝까지 실습하기
   1. 모두 따라하기까지 30분 정도 소요된다
   2. 매번 할 때마다 학습시간이 짧아지는 것을 느껴라
   3. 기억하기 보다, 기본 탐색과 편집 명령어들을 습관화하기
   4. (단순히 서버 환경에서 편집만 할 것이라면 이정도로 충분하다)
2. 최소한의 설정으로, 플러그인 없이 사용하기
   1. 최소한의 설정은 다음과 같다
   2. color scheme
   3. syntax highlighting
   4. spaces and tabs
   5. auto indentation
   6. line numbers
   7. tab completion(하위폴더 file 검색)
   8. insert 모드 빠른 진입을 위한 ESC 설정
3. 최소한의 플러그인으로 Vim 사용하기
   1. 핵심동작을 변경하지 않는 플러그인만 일단 사용하기
   2. auto-pairs.vim(brackets, parens, quotes를 쌍에 맞게 추가하거나 삭제해준다.)
   3. endwise.vim(Ruby의 경우 편하다.)
   4. ragtag.vim(HTML, erb 등의 tags에 도움이 된다.)
4. 동사와 명사를 활용한 Vim 명령어 사용하기
   1. Vim을 하나의 언어로 생각하고 새로운 명령어를 조합하자
   2. 이 내용은 다시 [이 글](https://medium.com/@jungseobshin/vim-%EB%B0%B0%EC%9A%B0%EB%8A%94-%EB%B2%95-4%EC%A3%BC-%EA%B3%84%ED%9A%8D-77f3f7e263f7)을 참고하자.

### Vim을 배우기 위한 도구들

- Vimtutor
  - Vim이 있으면 기본적으로 같이 딸려오는 튜토리얼
  - terminal에서 `$ vimtutor`
- [VIM Adventures](https://vim-adventures.com/)
  - 3레벨 이후로는 유료다. 거의 못함.
  - 하지만 hjkl 이동 감각 키우기에는 좋다.
- [Interactive Vim Tutorial](https://www.openvim.com/tutorial.html)
  - 웹 상에서 바로 가능한 튜토리얼이다
- 그 외에도 위의 '완전 초보를 위한 Vim' 글 맨 밑에 참고할만한 자료가 많다.

## Vim 학습 일지

### 1주차

- 200807(금)
  - 지루해서 하다말고 유튜브보고 다시 하고 하니까 거의 1시간 걸린 것 같다.. ㅎㅎ
  - 명령 모드가 파워풀한 것 같다. 익숙해지면 왜 빠르다고 하는지 알 것 같다.
  - 에디터를 나가지 않고 바로 터미널 명령을 사용하고, 결과를 출력한다던지 하는 것이 신기했다.
- 200811(화)
  - 7일만 채우면 사실상 1주차라고 생각한다 ㅎㅎ..
  - vim adventure이 무료가 3레벨까지인 것을 알아냈다.
  - vimtutor에 걸리는 시간이 정상적으로 바뀌었다. 30분내로 걸렸다.
- 200812(수)
  - 이거 꼭 vimtutor를 7일이나 해야할까..? 벌써 다 외워가기는 한다.
  - 그리고 변명같은데 그냥 VSCODE 쓰면 될거 같은데...
  - 오늘은 스피드런이었다 거의. 딱 20분정도 걸렸다.

> 200812 이후 ...
> 그렇게 열심히 이 계획을 따라서 할 줄 알았지만 ...
> vimtutor 하는 것이 지겨워 그만뒀다..

## 중도 포기 후 근황

200822,
지금까지 Vim은 계속 꾸준히 쓰고 있다.
Vimtutor은 지겨워서 매일 이것으로 연습하는 것은 그만 뒀다.

대신 Vim을 써야할 환경을 자꾸 만들었다.

### 1. Backend REST API 개발

현재 나는 Flask로 REST API 개발 프로젝트를 진행하고 있다.
이 과정에서 AWS CLI나 Docker CLI를 사용하기 때문에 터미널을 사용하는 경우가 많다.
그래서, 터미널을 열었을 때 문서를 수정할 일이 있으면 **대부분은 Vim을 사용해서 수정하면서 손에 익히려 노력했다.**

### 2. Git CLI

Windows 사용 시절 Git bash를 맨 처음으로 공부했지만,
어려워서 바로 GUI인 GitKraken을 사용했다.

하지만 이번 기회에 Git CLI를 다시 배워보기로 마음 먹었고,
**기본 에디터를 Vim으로 설정해서 커밋 메시지를 작성하고 있다.**

### 3. Dotfiles repo와 Shell script

[참고 링크](https://blog.appkr.dev/work-n-play/dotfiles/)
> dotfiles는 콘솔용 바이너리(e.g. gcc), 라이브러리, 애플리케이션의 설치 뿐만아니라, 그들의 설정을 잘 저장해 두었다가 컴퓨터를 빠르게 재구성하기 위한 워크플로우다.

나만의 dotfiles repo를 만들면서 쉘과 더 친해졌다.
쉘 스크립트를 짜서 설정 파일 업데이트를 자동화하기도 했는데,
이 과정에서 **쉘 스크립트 파일을 모두 Vim으로 작성하였다.**

> 결론적으로 ...
아직 Vim이 어렵다. 솔직히 VSCode가 편한거 같다.
하지만 Vim을 배우면서 **터미널과 Linux CLI와 빠르게 친해지는 것 같다.**
앞으로도 꾸준히 연습할 계획이다.
