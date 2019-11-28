---
title:  "Flask-marshmallow로 편하게 데이터~객체 관리하기"
excerpt: "serialize/deserialize/validation"
toc: true
toc_sticky: true

categories:
-   Python
tags:
-   Flask-marshmallow
last_modified_at: 2020-08-05TO22:30:00+09:00
---


### Flask-marshmallow

python 라이브러리 중 Marshmallow를,
Flask 마이크로 웹 프레임워크를 사용하는 프로젝트에서 더 사용하기 쉽게 만든
라이브러리이다.

### 간단 설명

Serialization이란,
python 객체 > JSON 문자열과 같은 것을 수행함.
> user_schema.dump(data)

Deserialization이란,
JSON 문자열 > python 객체와 같은 것을 수행함.
> user_schema.load(json)

Validation이란,
정해진 객체 구조에 맞게 JSON 문자열이 들어왔는지 확인함.
> user_schema.validate(json)

### Flask-sqlalchemy와의 호환성

같이 쓰면 좋다.
`class AuthorSchema(ma.SQLAlchemySchema):`
    `class Meta:`
        `model = Author`

    `id = ma.auto_field()`
    `name = ma.auto_field()`
    `books = ma.auto_field()`

Meta.model 로 db.Model을 넣어주면
자동으로 스키마 정보를 채워준다.
