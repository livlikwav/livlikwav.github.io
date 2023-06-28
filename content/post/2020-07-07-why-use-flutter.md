---
categories:
- Languages
date: "2020-07-07T00:00:00Z"
excerpt: 아는 만큼 보인다더니, 이제야 알게 되서 그렇답니다
last_modified_at: 2020-07-07TO22:30:00+09:00
tags:
- Flutter
- React-native
title: React-native 강의 결제 해놓고 Flutter 하게된 썰
toc: true
toc_sticky: true
---

Flutter로 하라는 눈치셨지만,
이미 React-native 강의를 결제했는 걸요...?
(이번에 Vue-native도 나왔다고 하셨다)

그래서 고민해봤다.

## 크로스플랫폼 대표주자 React-native와 Flutter

![react-native_logo](https://upload.wikimedia.org/wikipedia/commons/d/d3/React_Native.png)

React-native에 대한 대부분의 의견

- 가장 퍼포먼스가 안좋고
- 레이아웃 그리는게 힘들다
- 라이브러리가 많지만 오류도 많다
- 현재 약간 Deprecated의 길을 걷고 있다
  - Facebook이 더이상 관리를 잘 안해서, 패키지가 난무한다고 하셨다.

![flutter_logo](https://upload.wikimedia.org/wikipedia/commons/1/17/Google-flutter-logo.png)

Flutter에 대한 의견

- 그에 비해 구글이 관리를 잘 한다. 전담 팀이 있다
- UI를 화면 위에 그리는 방식
- 오류가 덜하고, 처음부터 많은 걸 지원한다
  - 리액티브는 여러개 갖다 붙여야함

## Web-RTC 라이브러리를 사용해야 한다면

일단 안전하게 가려면...

- 둘중에 개발자 커뮤니티가 잘 형성되어 있고 webrtc 라이브러리가 잘 되어 있는걸 선택
  - 하지만 둘다 라이브러리는 어느정도 안정적으로 지원

멘토님의 피드백

장기적으로 봤을때는 flutter도 충분히 매력이 있는건 맞다.
react native 프로젝트를 직접 수행하진 않고 리딩을 했었는데,
상용화 레벨의 서비스를 구축하는 과정에서 이슈가 꽤 많이 나왔었다.

flutter는 사용해보지 않아서 어느정도 레벨로 지원이 될지는 잘 모르겠지만
단순히 각 깃헙의 이슈 수를 봤을때, flutter의 이슈 수는 좀 비정상적이어서 우려스럽긴 하다.
깃헙 이슈수가 5000+ 는 처음 봤다-_-;

**보통 신규 라이브러리나 프레임웍 도입전에 이슈쪽을 먼저 보시면 감을 잡을수 있을 것이다.**
오픈되어 있는 이슈수와  closed된 이슈수, 그리고 최근의 이슈 수와 최근의 닫힌 이슈들 중에서
이번 프로젝트에 직접적으로 연관이 될것 같은 키워드를 서칭해서,
관련 이슈가 크게 없을것 같으면 도입을 시도해도 괜찮을것 같다.

아 그리고 이슈가 많다고 무조건 안좋은 프로젝트는 절대 아니다.
그만큼 커뮤니티가 활발하다는거니 판단을 내리려면 이슈들의 내용도 좀 확인해봐야 한다.

## 나의 선택은 Flutter

선택의 이유는,

- 현재 React-native, flutter 둘다 배우지 않은 상태라 지금 바꿔도 상관없다.
- 웹을 만들지 않아도 되고, 백엔드도 JS를 사용하지 않아도 된다.
  - 프론트엔드를 얼마나 빨리 개발해버릴 수 있는가가 제일 중요했던 점
- Flutter의 성장성을 보고 싶었다.
  - 구글에서 전담 팀까지 꾸릴 정도면 어느정도 밀어주는게 아닐까?
  - (혹자는 구글에서 그만큼 프로젝트를 잘 없애버린다고 하기도 한다, 참고)
- 개발 환경이 더 편하다고 한다.

### 참고글

- [Flutter, 왜 선택하지 못했나](https://engineering.linecorp.com/ko/blog/flutter-pros-and-cons/)