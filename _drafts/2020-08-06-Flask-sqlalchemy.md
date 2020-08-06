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
  - [Object States(Lifecycle)](#object-stateslifecycle)
  - [Event Handling 방법](#event-handling-방법)

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
- SQLAlchemy **Core**
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

[ORM Events에 대한 공식 소개 문서](https://docs.sqlalchemy.org/en/13/orm/session_events.html)
객체나 세션의 변화에 대해서 이벤트를 통하여 트래킹을 할 수 있다.
DB Trigger와 같은 것을, 이벤트, 이벤트 리스너 그리고 이벤트 핸들러로 구현할 수 있다.

나는 그 중 Object Lifecycle Events를 다뤄보기로 했다.
[Object Lifecycle Events](https://docs.sqlalchemy.org/en/13/orm/session_events.html#object-lifecycle-events)

위 이벤트를 다루기 위해서는 먼저, Object의 상태를 알아야 한다.

### Object States(Lifecycle)

[Quickie Intro to Object States](https://docs.sqlalchemy.org/en/13/orm/session_state_management.html#session-object-states)

Instance의 state는 다음과 같은 종류가 있다.

- Transient
  - session에 존재하지 않는 인스턴스
  - session.commit()해도 저장되지 않을 상태
  - session.add()해줘야 Pending 상태가 된다
- Pending
  - Session.add(transient instance)
  - 아직 flushed 되지 않은 상태
  - 다음 flush에 Persistent 될거임
  - session.commit()해주면 Persistent가 된다고 생각하면 된다
- Persistent
  - 세션에 있고, 디비에 저장된 상태
  - pending instances가 flushed하면 persistent 상태로 전이한다.
  - 또한 디비에서 querying 해온 인스턴스들이 persistent 상태이다.
- Deleted
  - pending state의 반대라고 생각하면 된다.
  - session.delete(instance)
- Detached
  - db 상의 레코드와 일치하는, 혹은 일치했던 인스턴스
  - 현재 아무런 세션에도 속하지 않은 상태

객체의 현재 상태를 받아오는 방법은 다음과 같다.

```python
from sqlalchemy import inspect
insp = inspect(my_object)
insp.persistent
# True
```

>일단 내 프로젝트에 실험을 해보자..

### Event Handling 방법

2가지 방법이 있다

1. @event.listens_for()
2. listen()

첫번째 방법

```python
from sqlalchemy import event

@event.listens_for(MyClass.collection, 'append', propagate=True)
def my_append_listener(target, value, initiator):
    print("received append evnet for target: %s" % target)
```

두번째 방법

```python
def validate_phone(target, value, oldvalue, initiator):
  return re.sub(r'\D', '', value)

listen(UserContact.phone, 'set', validate_phone, retval=True)
```

