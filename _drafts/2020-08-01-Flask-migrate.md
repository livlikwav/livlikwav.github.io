---
title:  "Flask-migrate : 아직은 필요성을 못 느낄만 했다"
excerpt: "커맨드를 관리하기 위한 라이브러리"


categories:
-   Flask
tags:
-   Flask-script
-   manage.py
last_modified_at: 2020-08-01TO22:30:00+09:00
---



### Database-migration 이란

마이그레이션이란, 한 운영환경으로부터 다른 운영환경으로 옮기는 작업을 뜻한다.
> Windows --> Linux

데이터베이스에서 데이터 마이그레이션이란, 데이터 베이스 스키마의 버전을 관리하기 위한 하나의 방법이다.
> 데이터 전환

작게는 프로젝트 상 테이블 생성 및 변경 작업부터, 하나의 애플리케이션 또는 시스템을 옮기는 것까지 마이그레이션이다.

열 이름을 바꾼다든지 하는 이력을 마이그레이션 코드로 남겨 두고 필요할 때마다 마이그레이션을 실행했다가 롤백하는 작업을 자유롭게 할 수 있다.

## flask-migrate

> Flask-Migrate is an extension that handles SQLAlchemy database migrations for Flask applications using Alembic. The database operations are made available through the Flask command-line interface or through the Flask-Script extension.

데이터베이스 마이그레이션이란, 운영환경의 전환을 위해서 데이터베이스의 버전관리를 수행하는 것이다. 내부적으로는 Alembic을 사용하는 것 같다.

[참고한 링크](https://blog.outsider.ne.kr/1143)
> Alembic은 SQLAlchemy 기반의 마이그레이션 도구로 Python을 사용하지만, 별도로 사용할 수 있으므로 프로젝트가 꼭 파이썬이거나 SQLAlchemy를 사용할 필요는 없다.

서비스를 운영하려다 보면 자연히 데이터베이스 스키마를 관리할 수 있는 마이그레이션 도구가 필요하다고 한다.

솔직히 감이 안잡히지만 일단 사용해보자! 다들 쓰기도 하고 Boilerplate 에도 나온다.