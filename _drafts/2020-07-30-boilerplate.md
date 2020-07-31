---
title:  "보일러플레이트: 그래서 어떻게 코딩을 시작해야할지 감이 안올때"
excerpt: "실제 예제 코드를 보고 code architecture, folder structure를 빨리 감잡기"


categories:
-  공부
tags:
-  보일러플레이트
-  boilerplate
last_modified_at: 2020-07-30TO22:30:00+09:00
---

[참고글](https://brunch.co.kr/@kooslab/144)
[참고글2]()

flask로 REST API 서버를 만들고 있다.
일단은 필요한 부분부터 빨리 찾아서 만들고 있는데,
모듈화를 못하겠어서 일단 파일 하나에 다 집어넣고 있었다.

이런 초보자들을 위해서 참고할만한 좋은 레퍼런스가 있다.
'보일러 플레이트'이다.

나는 다음과 같은 라이브러리를 사용한다.

- flask-sqlalchemy
- flask-marshmallow
- flask-restful

다음과 같은 예로 검색하면 github repo가 많이 나온다.
flask-sqlalchemy boilerplate

이걸 보고 대충 감을 잡으면 된다.