---
title:  "MacOS 터미널에서 바로 크롬 및 파인더 열기"
excerpt: "확실히 윈도우 쓰는 것보다 리눅스랑 빠른 속도로 친해지고 있다."


categories:
-   MacOS&Linux
tags:
-   macOS
last_modified_at: 2020-07-26TO22:30:00+09:00
---

- [터미널에서 바로 chrome 열기](#터미널에서-바로-chrome-열기)
  - [open 명령어](#open-명령어)
  - [이제서야 알게된 ~의 의미](#이제서야-알게된-의-의미)
  - [터미널 alias 설정](#터미널-alias-설정)
  - [source 명령어](#source-명령어)

사람들이 맥북을 추천하는 이유 중에는, 터미널이 좋다는 말이 있었다.
벌써 한 2달 가량 사용해 본 결과 맞는 말이었다!
터미널이 좋은 것보다, **리눅스와 TUI와 친해지고 있다**

마우스가 아니라, 고작 트랙패드로 손을 움직이는 것도 귀찮아졌다.
현재는 code 명령어를 잘 쓰고 있는데,
현재 위치에서 Finder를 열고 싶고, 원하는 url을 바로 chrome으로 띄우고 싶어졌다.

아마 1달 뒤쯤에는 vim이나 emacs를 배워서 쓰고있지 않을까 싶다.

## 터미널에서 바로 chrome 열기

먼저 리눅스 명령어랑 또 친해질 필요가 있다.
(MacOS 명령어와 100프로 일치하지는 않는다.)

### open 명령어

macOS의 터미널에서는 open이라는 명령어가 존재한다.
`open /path/to/some.app`
이와 같이 경로/프로그램명으로 작성하면 프로그램을 실행하고,
`open /Application/`
이와 같이 폴더경로만 작성하면 **해당 위치의 Finder가 열린다.**

리눅스에서는 현재 위치에서 파일을 열려면
`./abc`
와 같이 앞에 경로를 기술해주고, 뒤에 파일명을 작성하면 된다.
[참고 링크](http://ehpub.co.kr/%EB%A6%AC%EB%88%85%EC%8A%A4-%EC%8B%9C%EC%8A%A4%ED%85%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-3-2-open-close/)

### 이제서야 알게된 ~의 의미

[참고 링크](https://dasima.xyz/%EB%A6%AC%EB%88%85%EC%8A%A4-cd-%EB%AC%BC%EA%B2%B0-%ED%99%88-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC/)
홈 디렉토리였다 ^^
리눅스에 처음 로그인하면 접속하는 디렉토리가 홈 디렉토리고
보통 /home/사용자명

### 터미널 alias 설정

[참고 링크](https://onfriday.delfiini.co.kr/entry/Mac%EC%9D%98-%ED%84%B0%EB%AF%B8%EB%84%90%EC%97%90%EC%84%9C-alias%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%B3%84%EC%B9%AD-%EC%84%A4%EC%A0%95)
>alias(에일리어스)란? 단어 그대로 별칭을 뜻하고 이 명령어의 쓰임세는 Git, bower, npm 등을 사용하는 유저이거나, 리눅스 혹은 유닉스 계열 개발자일 경우 복잡하고 긴 명령어 + 옵션등을 간략하게 줄여서 쓸 수 있게 해주는 기능이라 생각하시면 됩니다. 예를 들면 리스트를 나타내는 명령문을 터미널에서 실행한다고 할 경우 ls 라는 명령어와 -al 옵션을 alias를 통하여 ll이란 별칭으로 등록한 경우 터미널에서 ll을 입력시 ls -al 이라고 친것과 동일한 결과값을 보여줍니다.

zsh 터미널을 사용하고 있다면 .zshrc를 열어준다
`code ~/.zshrc`

그리고 다음과 같이 terminal alias를 등록한다
`alias chrome='open -a /Applications/Google\ Chrome.app'`

저장해주고 나와서 설정을 적용해준다.
`source ~/.zshrc`

제대로 잘 됐다면 다음과 같이 확인해줄 수 있다.
`which chrome`

### source 명령어

[참고 링크](https://klero.tistory.com/entry/source-%EB%AA%85%EB%A0%B9%EC%96%B4%EB%9E%80)
>source 명령어는 스크립트 파일을 수정한 후에 수정된 값을 바로 적용하기 위해 사용하는 명령어이다.
예를들어 /etc/bashrc 파일을 수정 후 저장하여도 수정한 내용이 바로 적용되지 않는다.
왜냐하면 /etc/bashrc 파일은 유저가 로그인할 때 읽어들이는 파일이여서, 로그아웃 후 로그인하거나
리눅스를 재시작해야 적용이 된다.
이럴경우 간단하게 # source /etc/bashrc 명령어로 수정된 내용을 바로 적용할 수 있다.

.zshrc 파일이 쉘 스크립트 파일이다.
다음에는 **쉘 스크립트를 공부해봐야겠다.**
