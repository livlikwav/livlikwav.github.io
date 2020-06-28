﻿---
title:  "이클립스 디버거 사용하기"
excerpt: "그래도 printf가 더 편한거 같기도 하고.."

categories:
  - 툴
tags:
  - 자바
last_modified_at: 2020-04-07TO22:30:00+09:00
---

### 검색어
- 디버거
- 이클립스 디버깅

### 3줄요약
- **역시 개발자는 새로운 공부를 귀찮아 하면 안된다**
- 디버거를 왜 이제야 알았을까.. 그동안 printf 문 하나하나 넣는건 안 귀찮았나..
- 이런 의미로 Kotlin도 빨리 경험해보고, 오픈 API도 도전해보자.

### 디버거 - 위키피디아 > 개념 설명
[https://ko.wikipedia.org/wiki/%EB%94%94%EB%B2%84%EA%B1%B0](https://ko.wikipedia.org/wiki/%EB%94%94%EB%B2%84%EA%B1%B0)
- 디버거(영어: debugger) 또는 디버깅 도구(debugging tool)는 다른 대상 프로그램을 테스트하고 디버그하는 데 쓰이는 컴퓨터 프로그램이다
- 소프트웨어 버그나 유효하지 않은 값에 의해서 프로그램이 정상적으로 진행되지 않는 것을 트랩이라고 한다. 소스 레벨 디버거 또는 심볼릭 디버거의 경우 프로그램이 트랩되거나 정해진 조건에 도달하면, 디버거는 원본 코드에서의 위치를 보여준다. 요즘에는 대부분의 통합 개발 환경에서 볼 수 있다. 만약 로우 레벨 디버거 또는 기계어 디버거라면 이것은 디스어셈블리에서의 위치를 보여준다.
-  또한 프로그램을 차례로 실행하는 (single stepping 또는 프로그램 애니메이션), 멈추게 하는 (breaking) (브레이크포인트를 사용해서) 그리고 변수의 값을 추적하는 것 같은 좀 더 복잡한 함수들을 제공한다. 몇몇 디버거들은 실행 중인 프로그램의 상태를 수정하는 기능도 갖는다. 또한 논리적 에러나 충돌 시 다른 위치에서 실행을 계속할 수 있다.

### Eclipse 디버거 동영상 강의  (생활 코딩)
[https://opentutorials.org/course/3930/26662](https://opentutorials.org/course/3930/26662)
- 입문자일수록 개념을 적게, 도구는 많이 사용해야 합니다. 중급으로 나아갈수록 지식의 양이 기하급수적으로 늘어납니다. 이때 스스로 모르는 것을 찾아내기 위해서는 도구가 필요합니다. 정말 유용한 도구인 디버거를 소개합니다.
- (내 생각) 도구를 많이 사용하며 흥미를 잃지 않되, 전공생이라면 개념을 자꾸 찾아보고 API 문서와 친해지기.

### Eclipse 디버거 텍스트 강의 + 사용 사례
[https://spoqa.github.io/2012/03/05/eclipse-debugger.html](https://spoqa.github.io/2012/03/05/eclipse-debugger.html)
- 꽤 많은 분들이 디버거의 존재 자체를 모르고 있거나 혹은 디버거가 있다는 사실은 알아도 그 효용성에 의문을 제기하곤 합니다. 왜냐하면, 우리에겐 `Log` 클래스나 혹은 `printf`같은 훌륭한(?) 디버깅 도구가 있다고 생각하기 때문이죠. 물론 이렇게 필요한 변수를 찍어보면서 어떤 곳에서 버그가 있는지를 알아보는 일이 잘못된 일은 아닙니다만 **복잡한 여러 상황이 맞물려 재현되는 버그는 이러한 고전적인(?) 방법을 써서 알아보기가 매우 어렵습니다**.
- 원인을 정확히 그리고 빨리 파악하려면 디버거의 사용법을 숙지하고 사용하는 것이 가장 좋습니다. 대부분의 개발 환경에서 디버거를 제공하는데 다행히 [이클립스](http://www.eclipse.org/)에서도 쓸만한 디버거를 내장하고 있습니다.
- 보통 디버깅을 할 때 가장 먼저 하는 일이 브레이크 포인트를 잡는 일입니다. 브레이크 포인트를 **에러가 일어나는 라인이나 혹은 의심이 가는 변수를 추적할 수 있는 라인쯤**에 잡아놓고 프로그램을 디버깅하면 해당 라인을 실행할 때 디버거가 작동하게 되고 그곳에서 프로그램을 라인 별로 진행해가며 관찰을 진행할 수 있게 됩니다.
- 지정한 브레이크 포인트에 다다르면 동시에 디버거가 작동하게 되고 그 라인부터 스텝 단위의 진행을 할 수 있게 됩니다.
- 이제 이 뷰의 버튼들을 이용하여 현재 상황을 진행하거나 되돌릴 수 있습니다. 자주 사용하는 버튼의 사용법을 알아보면

1.  Resume : 다음 브레이크 포인트를 만날때까지 진행합니다.
2.  Suspend : 현재 작동하고 있는 쓰레드를 멈춥니다.
3.  Terminate : 프로그램을 종료합니다.
4.  Step Into : 메서드가 존재할 경우 그 안으로 들어가 메서드 진행 상황을 볼 수 있도록 합니다.
5.  Step Over : 다음 라인으로 이동합니다. 메서드가 있어도 그냥 무시하고 다음 라인으로 이동합니다.
6.  Step Return : 현 메서드에서 바로 리턴합니다.
7.  Drop to Frame : 메서드를 처음부터 다시 실행합니다.

등이 있습니다.
- **디버깅을 진행하는 도중 변수의 값이나 객체의 상태를 알고 싶은 상황**이 생기게 됩니다. 현재 의심이 가는 변수 이외에도 이 변수에 영향을 끼칠 다른 변수들이나 객체들의 상황을 실시간으로 검사할 필요가 있을 때 **변수 뷰**를 이용하면 도움을 얻을 수 있습니다.
- 이곳에서 변수나 객체의 상태를 확인하고 변수의 상황에 대해서 저장할 수 있습니다. 변수나 객체의 상황을 모두 저장해서 클립보드에 붙이고 싶은 일이 생기면 해당 변수를 오른클릭 후 Copy Variables를 선택합니다.
- 변수를 Expression 뷰로 보내게 되면 이곳에서 지속해서 변수의 상태를 관찰할 수 있게 됩니다.
- **브레이크 포인트에 조건을 거는 것**이 굉장히 유용할 때가 있습니다. 특히 **반복문안에 들어가 있는 코드들을 디버깅할 때 **유용하지요. 반복문의 경우 모든 상황을 검사한다기보다는 특정 조건에서 값이 어떻게 들어가는지를 분석하는 경우가 더 많은데 이러한 상황을 검사하기 위해서 브레이크 포인트에 조건을 걸어야 합니다.
- 브레이크 포인트를 거는 과정까지는 똑같습니다. 브레이크 포인트를 건 후 **그 포인트에서 오른 클릭을 하면 Breakpoint properties 옵션**이 있는 것을 확인할 수 있습니다. 이 옵션에서 조건문을 설정하여 디버거의 활성화 조건을 설정할 수 있습니다.
- 먼저 `Conditional`을 활성화하여 어떤 조건에서 디버깅 화면으로 전환할지를 쓰면 되는데 이 창에 조건식을 쓰면 됩니다.
- 또 `hit count`를 이용하여 조건을 걸 수도 있습니다. `hit count`에 값을 적용하면 해당 라인에 브레이크 포인트가 `hit count`만큼 잡힌 이후 디버깅 화면으로 전환하게 됩니다. `hit count` 옵션은 반복문에서 한 100번쯤 이후에 디버깅을 시작하고 싶거나 하는 일이 생길 때 유용하게 쓸 수 있습니다.

### 간단한 예제코드가 있길래..
[https://codedragon.tistory.com/6137](https://codedragon.tistory.com/6137)
- 설명이 달라서 더 잘 읽힐 수도 있겠다.