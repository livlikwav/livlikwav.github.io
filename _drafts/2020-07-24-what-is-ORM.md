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

## 결국 공식 문서가 최고다

맨 처음에는 너무 오래걸릴까 겁나하고 피하게 되는데, 결국은 공식 문서가 최고인 것 같다.
[https://docs.sqlalchemy.org/en/13/intro.html](https://docs.sqlalchemy.org/en/13/intro.html)


### Overview

SQLAlchemy has two major components

- SQLAlchemy ORM
- SQLAlchemy Core
  - Schema / Types
  - SQL Expression Language
  - Engine
    - Connection Pooling
    - Dialect

New users should begin with Object Relational Tutorial

### Object Relational Tutorial

### Domain model, DDD

Domain = field that has problem
Domain model describes ...

- various entities
- their attributes
- roles
- relationships
- constraints

### Connecting

- create_engine()

echo flag
> shortcut to setting up SQLalchemy logging
> enabled, can see all the generated SQL produced

return value of create_engine()
> instance of Engine
> core interface to the database
> adapted through a dialect, DBAPI

Engine.execute() or Engine.connect()
> engine establishes a real DBAPI connection to the database

When using the ORM, we typically don't use the Engine directly one created

### Declare a Mapping

configurational process

1. describing the database tables
2. defining our own classes

In modern SQLAlchemy, these two tasks are usually performed together
using a system 'Declarative'

Declarative
> allows us to create classes that include directives to describe the actual database table

mapped class inherit declarative base class
`Base = declarative_base()`

in mapped class, we define details about the table
> mapped class = table
> table name, names, datatypes of columns

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key = True)
    name = Column(String)
    fullname = Column(String)
    nickname = Column(String)

__repr__() method
this is optional
we only implement it in this tutorial
this method be used to nicely format User object

declarative replaces
all the Column objects >> descriptors(__get__, __add__, __delete)
this process called instrumentation

the instrumented mapped class persist and load the values of cols from the db

the class also remains mostly a normal python class
> we can define any number of ordinary attributes and methods

### Create a Schema

class via the Declarative system
this is about our table, known as table metadata

Table object
represent table metadata for a specific table

we can see this Table object
by inspecting the __table__ attribute

`User.__table__`

diffirent way (!= Declarative system)
mapped to any Table using the mapper() func directly

but Declarative system is highly recommended

VARCHAR columns
> only allowd on SQLite and PostgreSQL
> use String(50)

Sequence()
> 이거는 Oracle이나 Firebird에서 쓰는 다른 새로운 primary key idenfiers를 위한 옵션인듯

### Create an Instance of the Mapped Class

with mappings complete
now create and inspect a User object

지금까지 클래스를 만든거자나.
이제 객체를 만들어야해. 클래스로 인스턴스 빵 구워내야해.

>>> ed_user = User(name = 'ed', fullname='Ed Jones', nickname = 'edsnickname')
>>> ed_user.name
'ed'
>>> ed_user.nickname
'edsnickname'

Declarative system - __init__() method
free to define any explicit __init__()
there is default __init__()
automatically accepts keyword names that match the columns we've mapped

id attribute
SQLAlchemy's instrumentation normally produce this default value 'None'
produce when first accessed

instrumentation system is tracking attributes of mapped class
emit INSERT statement when assign something on attributes

### Creating a Session

now ready to start talking to the DB
The ORM's "handle" to the db is the Session

at the same level as our create_engine() statement,
we define a Session class
which will serve as a factory for new Session objects

from sqlalchemy.orm import sessionmaker
Session = sessionmake(bind = engine)

This custom-made Session class will create new Session objects
which are bound to our database.

Whenever you need to have a conversation with the db,
you instantiate a Session
`session = Session()`
but it hasn't opened any connections yet

### Adding and Updating Objects

ORM object = record of table

to persist our User object
we Session.add() it to our Session

why ORM is persistence technology?
because we want to persist our object

`ed_user = User(name=~)`
`session.add(ed_user)`

pending > flush

we create a new Query object which loads instances of User
`our_user = session.query(User).filter_by(name='id').first()`
> get first result in the full list of rows

Session identify that the row returned is the same row as one already represented within its internal map of objects
`ed user is our user`
`True`

identity map
> a mapping between python objects - database identities
> a collection that is associated with an ORM session object
> maintain a single instance of every db object keyed to its identity

ensure that all operations upon a particular row
within a Session operate upon the same set of data

add more User objects
using add_all()
`session.add_all([User(), User(), User()])`

session is paying attention
it knows what is modified
`session.dirty`

and knows what is pending
`session.new`

we'd like to issue all remaining changes to the db
and commit the transaction
we use Session.commit()
`session.commit()`
flushes the remaining changes to the db
and commits the transaction

connection resources referenced by the session
are now returned to the connection pool

after commit session,
mapped object now has a id value
`ed_user.id`
`1`

### Rolling Back
we can roll back changes made too

session에 있는 ed.user를 update 하고
새로운 object를 만들어서 session.add() 하고나서 
rollback = 가장 최근의 session commit 상태로 돌아갈 수 있음

## 블로그 참고

데이터베이스 > 테이블 > 레코드 순서인데
Base로 만든 Class가 테이블
Class로 만든 instance가 레코드라면
데이터베이스는 어떻게 만들지?