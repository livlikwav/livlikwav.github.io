---
title:  "ORM이란?"
excerpt: "SQLMapper to ORM"


categories:
-  DB
tags:
-  ORM
last_modified_at: 2020-07-24TO22:30:00+09:00
---

이번에 처음으로 그럴듯한 백엔드 프로젝트를 수행하면서 웹 서버와 DB를 연동하게 되었다.
(이것도 안해봤다니 역시 학교만 다니면 프로그래밍 실력은 안는다... 진작 한이음 같은 거라도 할걸)

Flask와 Mysql을 사용해서 개발을 진행하게 되었다.
역시나 유튜브가 제일 도움이 되었다. 코드를 어떻게 작성하는지가 바로바로 보이니까 이해가 빠르다.
'Flask mysql' 이런식으로 검색해서 인도 프로그래머 행님 강의를 보았다.
SQLAlchemy, Marshmellow ... 이런 처음 보는 것들이 나와서 검색해보다가 ORM이라는 것을 알게 되었다.

그래서, 이번에는 SQLAlchemy를 쓰게 되었다.
그래서 ORM이 무엇인지 간단하게 정리하고 넘어가려고 한다.
어떻게 해서 나오게 되었는지.

> 여담인데 예전에 부스트코스에서 웹 풀스택 강의를 혼자 수강했었다. 그때도 JDBC라는 것을 배웠었는데 하나도 기억하지 못하고 있었다. 그리고 앞의 많은 부분을 공부하다가 정작 중요한 파트가 나올때 힘이 빠져서 Spring도 맛보지 못하고 그만 뒀던 기억이 있다. 프로그래밍에 있어서는, 나에게는 가장 상위 레벨의 최신 기술로 훑고, 전체 그림을 보고 나서 필요한 부분을 하나하나씩 파는게 맞는 것 같다.

### 참고한 영상

- [https://youtu.be/mezbxKGu68Y](https://youtu.be/mezbxKGu68Y)
- [https://youtu.be/B6iOqljc7U8](https://youtu.be/B6iOqljc7U8)
- [https://www.youtube.com/watch?v=6mHpfGjpE_M](https://www.youtube.com/watch?v=6mHpfGjpE_M)

## ORM = Object Relation Mapping

보통 DB 연동시
코드를 돌리는게 있고 
데이터를 쿼리를 하거나 할때 
SQL statement로 해서 호출을 한다.

DB는 굉장히 역사가 오래된 시스템이다.
굉장히 많은 양의 데이터를 굉장히 효율적으로 검색을 할 수 있게 해주는 기술이다.

언제나 DB에 저장되는 데이터는 1차원적이다.

광장히 이질적인 패러다임 2개를 같이 쓰게 된다.

- OOP
- ER

DB쪽의 입장이 아니라 Programmer 입장에서 모든 걸 생각해보자.
Object 안에 composition으로 다른 객체 참조가 되게 되어있다. 이게 외래키랑 비슷하다.

또 다른 레이어를 만들자.
프로그래머는 객체로 저장하면
뒤에 SQL, NoSQL(JSON), File 다 저장해준다.
쿼리를 알 필요도 없다.

성능적인 문제가 있긴 하다
stored procedure와 같은 혜택을 받기는 어려워서 적용은 늦었따.

DB를 만들때 SQL query를 써서 직접 생성하지 않는다.
ORM을 쓴다.

만약에 기존에 존재하는 데이터베이스가 있을 경우에는,
거기에 맞게 코드를 작성하는게 낫다.
DB first method

이제 나아가는 방법
Code first method

똑같은 개념으로 JSON도 말한다
JSON도 Object에서 생성을 하는게 맞다.

결과적으론 Object를 기반으로 프로그래밍하는 날이 왔다.
