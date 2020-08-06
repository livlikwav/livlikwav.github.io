---
title:  "Flask-sqlalchemy Events 다루기"
excerpt: "DB Trigger와 같이 ORM에서도 이벤트를 다루는 방법에 대해 알아봅니다."


categories:
-  Flask
tags:
-  SQLAlchemy
-  Flask-SQLAlchemy
last_modified_at: 2020-08-06TO22:30:00+09:00
---
- [Flask-SQLAlchemy 간단 소개](#flask-sqlalchemy-간단-소개)
  - [Persistence](#persistence)
  - [SQLAlchemy](#sqlalchemy)
  - [Flask-SQLAlchemy](#flask-sqlalchemy)
- [ORM Events](#orm-events)
  - [Attribute Events](#attribute-events)

## Flask-SQLAlchemy 간단 소개

### Persistence

DB를 연동한다는 것은 결국 프로그램에서 데이터를 저장하기 위함이다.
그리고 이러한 기술을 보통 Persistence 기술이라고 한다.

그 중 제일 트렌디한 기술이 ORM인데,
SQLAlchemy는 Python 진영의 대표적인 ORM이다.

ORM이란 Object-Relation Mapping이다.
SQL Mapper에서는 결국 SQL문으로 DB를 다루지만,
ORM은 Object-Oriented Programming의 장점을 그대로 가져가기 위해서
SQL문을 자동으로 생성해준다.

### SQLAlchemy

[SQLAlchemy 공식문서](https://docs.sqlalchemy.org/en/13/intro.html)
SQLAlchemy는 2가지의 중요 구성 요소가 존재한다.

- SQLAlchemy ORM
- SQLAlchemy Core
  - Schema / Types
  - SQL Expression Language
  - Engine
    - Connection Pooling
    - Dialect

### Flask-SQLAlchemy

SQLAlchemy의 Flask 지원 확장판이 Flask-SQLAlchemy이다.
[Flask-SQLAlchemy 공식문서](https://flask-sqlalchemy.palletsprojects.com/en/2.x/)

좀 더 코드가 간결해지고, Flask-Marshmallow 등과 함꼐 사용하면 편리하다.

## ORM Events

### Attribute Events

`class sqlalchemy.orm.events.AttributeEvents`
객체 속성에 대해서 이벤트를 정의할 수 있다.

첫번째 방법

```python
from sqlalchemy import event

@event.listens_for(MyClass.collection, 'append', propagate=True)
def my_append_listener(target, value, initiator):
    print("received append evnet for target: %s" % target)
```

