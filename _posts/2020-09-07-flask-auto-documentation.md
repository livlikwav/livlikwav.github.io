---
title:  "Flask REST API 문서 자동화 하기, Flasgger"
excerpt: "Swagger JSON과 UI를 지원하는 라이브러리인 Flasgger, 그리고 flask-apispec과 flask-restful-swagger 실패 기록까지"
toc: true
toc_sticky: true

categories:
-  Flask
tags:
-  Swagger
last_modified_at: 2020-09-07TO20:30:00+09:00
---

## 결론

Flasgger를 적용하여 API 문서 작성.

- 현재 Flask와 Flask-restful, Flask-sqlalchemy를 이용해서 REST API를 개발
- Swagger UI version 3과 OAS 3.0을 지원하는 Flasgger라는 라이브러리를 통해 API 문서를 작성
- 실제 프로젝트 소스에 적용하기 전에는 Swagger UI Editor라는 웹 OAS 에디터를 통해 작성
- Spring에 Swagger를 적용하는 것처럼 **'문서 자동화는 이루지 못함'(메소드별 자동 yml 매핑 정도..)'**
  - 하지만 프로젝트 내부에 Docs 파일도 함께 관리할 수 있음에 감사

> 사용방법은 뒤에 ...

## 문서화의 필요성을 여실히 느끼다

- 지금까지 Flask로 REST API를 개발함
- Swagger UI Editor로 OAS 3.0으로 설계 문서 작성함
- Swagger가 Spring 진영에서 사용한다고 하여 Swagger JSON, UI 도전 안함.
- Postman으로 API 테스트를 수행하였고, Publish Docs 기능을 이용해서 문서화 진행
  - 하지만, 특정 메소드의 변화가 반영되지 않는 문제점이 있었음.
- 또한 명확한 문서 유지 보수 필요성을 느낌
  - 클라이언트 개발 팀원에게 API 문서를 전달해야함
  - 설계 수정을 해야하는데 문서가 없으면 한눈에 보기가 어려움
- 그래서 결국 Auto Documentation을 할 방법을 다시 찾아봄.

> 느낀점 : 처음에 문서 유지 보수 생각을 잘 하고 문서화 잘 해놓자.
> 안그래도 할게 많은데 문서를 다시 작성하는 것은 너무 귀찮았고,
> 또 초기 설계대로 되는 법이 없어서 무조건 고치게 된다.

## Flask auto documentation

'Flask 문서 자동화'나 'Flask auto documentation'이라고 검색하면,
라이브러리가 나오지 않거나 Flask-apispec이 나온다.
'Flask Swagger'등의 다른 키워드로 검색을 해도 Star가 높은 repo는 나오지 않는다.

내가 찾았던 방법들은 다음과 같다.

- Flask-restplus
- Flask-restful-swagger
- Flask-apispec

> 이외의 라이브러리도 다 400~600 대의 Star였다.

### Flask-restplus

Flask의 REST 개발 라이브러리로 크게 2가지가 있다.
Flask-restful과 Flask-restplus이다.

나는 restful이 코드가 간결해보여서 택했는데, restful은 swagger를 기본적으로 지원해주지 않았다.

하지만 restplus는, 별다른 세팅없이 개발한대로 자동으로 문서화 되도록 지원이 잘 되어있었다.
더불어서, 참고할 한글 블로그 글도 있었다.

따라서 아직 Flask REST API 개발을 시작하지 않았다면 Flask-restplus도 고려해보길 바란다.

### Flask-restful-swagger

현재 Flask-restful을 사용하고 있어서, 이 라이브러리를 위한 Swagger 라이브러리를 먼저 찾았다.

[Flask-restful-swagger repo](https://github.com/rantav/flask-restful-swagger)
> flask-restful-swagger is a wrapper for flask-restful which enables swagger support.
In essence, you just need to wrap the Api instance and add a few python decorators to get full swagger support.

Star는 600개 정도, 가장 최근 커밋이 3 months ago 였다.
Issue를 먼저 확인했다.

![image](https://user-images.githubusercontent.com/44190293/92328268-69dde100-f09a-11ea-9b01-5888377299ca.png)
Python 3.8에 대한 2018년에 작성된 Issue가 있었는데, 아직까지 답변이 없었다.
내가 3.8로 개발하고 있어서 약간 쎄했다.

![image](https://user-images.githubusercontent.com/44190293/92329280-829dc500-f0a1-11ea-8115-5b6df122dccf.png)
예제 코드를 보니, @swagger.operation으로 메소드에 데코레이터를 달고, 추가적인 정보를 넣을 수 있었다.
Model에는 @swagger.model 데코레이터만 달면 되었다.
간단해 보였다.

### flask-restful-swagger 실패

예상되는 원인은, 해당 라이브러리의 Factory pattern에 대한 지원이 없는 것 같았다.
init_app()를 검색해보았지만, 검색 결과가 없었다.

```python
    api.init_app(app)
    # Set up flask-restful-swagger
    api = swagger.docs(api,
    apiVersion='0.1',
    basePath="http://localhost:5000",
    resourcePath="/",
    description="A Basic API"
    )
```

위와 같이 그냥 해보았지만, 웹 상에 Swagger UI 자체가 렌더링되지 않았다.
> /api/spec, /api/spec.json, /api/spec.html 다 404 Error...

### Flask-apispec 보류

다음으로 찾은, Flask auto documentation이라고 검색하면 가장 먼저 나오는 library였다.
가장 최근 커밋이 9 days ago 였지만, 역시나 Star는 400개 정도 였다.

[Flask-apispec repo](https://github.com/jmcarp/flask-apispec)
> flask-apispec is a lightweight tool for building REST APIs in Flask. flask-apispec uses webargs for request parsing, marshmallow for response formatting, and apispec to automatically generate Swagger markup. You can use flask-apispec with vanilla Flask or a fuller-featured framework like Flask-RESTful.

예시 Quickstart 코드는 다음과 같다.

```python
from flask import Flask
from flask_apispec import use_kwargs, marshal_with

from marshmallow import Schema
from webargs import fields

from .models import Pet

app = Flask(__name__)

class PetSchema(Schema):
    class Meta:
        fields = ('name', 'category', 'size')

@app.route('/pets')
@use_kwargs({'category': fields.Str(), 'size': fields.Str()})
@marshal_with(PetSchema(many=True))
def get_pets(**kwargs):
    return Pet.query.filter_by(**kwargs)
```

다음과 같은 이유로 이 라이브러리는 사용을 보류했다.

- Flask-restful을 지원한다고 하지만 설명이 부족하다(예시 코드를 찾을 수 없다)
- 사용하지 않고 있는 webargs 라는 라이브러리를 사용한다
- 사용하지 않고 있는 use_kwargs, marshal_with 데코레이터를 사용한다.

## Flasgger

그리고..**마지막으로 Flasgger를 찾았다. Star가 2.3k였다. README.md 마저 깔끔했다(눈물).**
![flasgger](https://github.com/flasgger/flasgger/raw/master/docs/flasgger.png)
[Flasgger repo](https://github.com/flasgger/flasgger)
> Easy OpenAPI specs and Swagger UI for your Flask API

README.md와 examples 코드들이 빠방했고, issue와 stack-overflow도 검색 결과가 있었다.
그 결과로, (위에 작성한대로) Flasgger를 사용하기로 결정하였다.

나름대로 정리한 소개 및 사용법은 다음과 같다.

### 소개

- Swagger UI 2와 3 모두 지원
- OpenAPI version 2와 3 모두 지원
  - 하지만 OAS 3.0은 Stable하지 않은 것 같다(Still experimental)
- `pip install flasgger`로 다운로드 할 수 있다
- Flask-restful 라이브러리를 지원하고 예제 코드도 있다.
- Factory pattern(init_app())을 지원한다.
- Validation도 지원한다.

### 사용법

README.md 에서는 크게 다음과 같이 나누고 있다.

- Using docstrings as specification
- Using external YAML files
- Using dictionaries as raw specs
- Using Marshmallow schemas

이 중에서 나는 external YAML file을 작성해서 사용하고 있고,
Flask-restful의 Resource를 yml 파일과 자동 매핑해주는 기능과 doc_dir 설정을 사용하고 있다.

### OAS 3.0 설정

기본 설정이 OAS 2.0 spec이므로 따로 설정해줘야한다.

나는 config.py를 별도로 작성하여 app 생성시에 적용해주고 있다.

```python
# project/swagger.py

swagger_config = {
    'openapi': '3.0.0',
    ...
}
```

```python
# project/config.py

class Config:
    # flasgger config
    from swagger import swagger_config
    SWAGGER = swagger_config
```

```python
# project/app/__init__.py

db = SQLAlchemy()
ma = Marshmallow()
api = Api()
swagger = Swagger(template=swagger_template, parse=True)

def create_app(config):
    app = Flask(__name__)
    config_name = config

    if not isinstance(config, str):
        config_name = os.getenv('FLASK_CONFIG', 'default')

    app.config.from_object(Config[config_name])

    # Set up extensions
    db.init_app(app)
    ma.init_app(app)
    api.init_app(app)
    swagger.init_app(app)

    return app
```

### doc_dir 설정

Flask-restful의 Resource의 메소드마다 docstring으로 작성하는 것이 아니라,
yml 파일이 들어갈 폴더를 만들어서, Swagger()에 설정해놓으면 자동으로 매핑해준다.

- 예시 Resource

```python
class LoginApi(Resource):
    def post(self):
        ...
        return '', 200
class LogoutApi(Resource):
    @confirm_account
    def post(self):
        ...
        return '', 200
```

- config에 다음과 같이 디렉토리를 지정해준다.

```python
# project/swagger.py

swagger_config = {
    'doc_dir': './app/docs/'
    ...
}
```

- project/app/docs/ 디렉토리와 파일을 다음과 같이 만들어 준다.
  - yml파일은 post, get, put, delete 맡게 적어준다.

![image](https://user-images.githubusercontent.com/44190293/92398890-5008d080-f164-11ea-940d-a59de0a07a69.png)

- post.yml을 OAS 3.0에 맞게 작성해준다.

```yaml
# project/app/docs/LoginApi/post.yml

tags:
  - user
summary: Logs user into the system
responses:
  "200":
    description: successful operation
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/user_auth_token"
  "401":
    description: Invalid useremail/password supplied
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/api_fail_response"
requestBody:
  content:
    application/json:
      schema:
        $ref: "#/components/schemas/login_user"
  description: Login user object
  required: true
```

- localhost:5000/apidocs에서 확인할 수 있다.

![image](https://user-images.githubusercontent.com/44190293/92399401-33b96380-f165-11ea-92e6-4a3f071e0893.png)
