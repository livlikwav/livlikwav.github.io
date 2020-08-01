---
title:  "Flask 기반 REST API 개발 도전기"
excerpt: "일단 만들어놓고 혼나면서 수정한다. 구르면서 모르는걸 배운다."


categories:
-  백엔드
tags:
-  Flask
last_modified_at: 2020-07-26TO22:30:00+09:00
---

## Flask-sqlalchemy

SQLAlchemy의 Flask에 특화된 버전인 Flask-sqlalchemy를 사용했다. 처음에는 디비 코드도 싹다 app.py에 넣었다. 애초에 어떻게 모듈화 해야할 지 모르겠더라.


## config.py

- Config
- DevConfig(Config)
- TestConfig(Config)
- ProductionConfig(Config)
- ...

와 같이 Configuration을 위한 변수들을 각각 클래스로 선언해서 사용한다.

## factory pattern으로 app 생성하기

```def create_app(config=None):

    app = Flask(__name__)
    if config is not None:
        app.config.from_pyfile(config)
    # configure your app...
    return app
```


- Api Versioning
- Api Resource

GraphQL
리소스를 정의하고 
리소스를 결합해서 쿼리할 수 있는 형태

이걸 제일 잘 만들어 놓은 회사가 페이스북이다.

GraphQL이 트렌디한 기술인가보다

reference 하기 가장 좋은 API는 페이스북
만약에 금융권에 있다하면 페이팔 API임
> 페이팔 API는 정말 아름답다고 하심

가장 배우기 쉬운것은 좋은 API를 베끼자

- 페이스북
- 페이팔