---
title:  "Flask-script : manage.py는 뭘까?"
excerpt: "커맨드를 관리하기 위한 라이브러리"


categories:
-   Flask
tags:
-   Flask-script
-   manage.py
last_modified_at: 2020-08-01TO22:30:00+09:00
---

- [flask_script](#flask_script)
  - [manage.py](#managepy)

[flask_script 공식 문서](https://flask-script.readthedocs.io/en/latest/)
> The Flask-Script extension provides support for writing external scripts in Flask. This includes running a development server, a customised Python shell, scripts to set up your database, cronjobs, and other command-line tasks that belong outside the web application itself.

웹 어플리케이션 모듈 밖에서 스크립트를 관리해주는 라이브러리이다. 다음과 같은 기능을 포함한다.

- 개발 서버를 실행한다.
- 파이썬 쉘을 커스터마이징한다
- 데이터베이스를 세팅하기 위한 스크립트를 작성한다 등

많이 보이던 manage.py를 위한 라이브러리이다.

## Creating and running commands

첫번째 과정은 스크립트 명령을 실행하기 위해 파이썬 모듈을 만드는 것이다. 그리고 대부분의 경우 이름을 manage.py로 짓는다.

꼭 하나의 manage.py 파일만 만들어야 할 필요는 없다. 프로젝트가 크다면 관리해야할 명령도 많기 때문에 여러 파일로 만들면 된다.

### manage.py

manage.py 파일에서 Manager 클래스의 인스턴스를 만든다. Manager 클래스는 모든 명령을 관리하고, 커맨드라인에서 어떻게 호출될지를 관리한다.

`from flask_script import Manager`
`app = Flask(__name__)`
`manager = Manager(app)`
`if __name__ = "__main__":`
    `manager.run()`

`manager.run()`을 호출하는 것은 Manager 인스턴스가 커맨드 라인의 입력에 반응하도록 대기시킨다.

명령을 추가하는 방법은 3가지가 있다.

- Command class를 상속하는 것
- @command 데코레이터를 사용하는 법
- @option 데코레이터를 사용하는 법

근데 이 중에서 @command 사용하는 것이 가장 심플하다.
`@manager.command`
`def hello():`
    `print "hello"`

옵션도 추가할 수 있다.
`@manager.option('-n'. help='Your name')`
`def hello(name):`
    `print "hello", name`

## Flask-base 의 manage.py를 보고 사용법 익히기

1. 공식 문서를 쭉 훑고
2. Flask의 boilerplate인 Flask-base repo의 manage.py를 보고 감을 잡자

[Flask-base, manage.py](https://github.com/hack4impact/flask-base/blob/master/manage.py)
