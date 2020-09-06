---
title:  "Flask에서 문서 자동화 하기, Flask-apispec"
excerpt: "OpenAPI 기반으로 자동으로 REST API 문서화를 도와주는 Swagger를 Flask에 적용해봅시다."
toc: true
toc_sticky: true

categories:
-  Flask
tags:
-  Swagger
last_modified_at: 2020-09-05TO20:30:00+09:00
---

## 서론

- 지금까지 Flask로 REST API를 개발함
- Swagger UI Editor로 OAS 3.0으로 설계 문서 작성함
- Swagger가 Spring 진영에서 사용한다고 하여 Swagger UI 찾아보지도 않고, 사용하지 않음
- Postman으로 API 테스트를 수행하였고, Publish Docs 기능을 이용해서 문서화 진행
  - 하지만, 특정 메소드의 변화가 반영되지 않는 문제점이 있었음.
- 더불어, 클라이언트 개발 팀원에게 API 문서를 전달해야할 일이 생겨서 다시 문서화 유지 보수 필요성이 생김.
- 그래서 다시 Auto Documentation에 대한 고민을 하게됨.

문서 자동화의 필요성을 알 수 있는 좋은 기회였다.
안그래도 할게 많은데 문서를 다시 작성하는 것은 너무 귀찮았고,
또 초기 설계대로 되는 법이 없어서 무조건 고치게 된다.

## Flask auto documentation

Flask에서의 REST API 개발을 돕기 위한 라이브러리로 크게 2가지가 있는 것 같다.
Flask-restful과 Flask-restplus.
나는 restful이 코드가 간결해보여서 택했는데, restful은 swagger를 기본적으로 지원해주지는 않았다.
restplus는 별다른 세팅없이 개발하면 문서화도 자동으로 되도록 지원이 잘 되어있었던 것 같다.

### Flask-restful-swagger

[Flask-restful-swagger repo](https://github.com/rantav/flask-restful-swagger)
> flask-restful-swagger is a wrapper for flask-restful which enables swagger support.
In essence, you just need to wrap the Api instance and add a few python decorators to get full swagger support.

Flask-restful을 위한 Swagger 라이브러리도 있었다.
Star는 600개 정도, 가장 최근 커밋이 3 months ago 였다.
Issue를 먼저 확인했다.

![image](https://user-images.githubusercontent.com/44190293/92328268-69dde100-f09a-11ea-9b01-5888377299ca.png)
Python 3.8에 대한 2018년에 작성된 Issue가 있었는데, 아직까지 답변이 없었다.
일단 쎄해서 Flask에서 공식적으로 지원하는 것 같은 라이브러리는 없나 더 찾아보았다.

### Flask-apispec

Flask auto documentation이라고 검색하면 가장 먼저 나오는 library였다.
Star는 400개 정도이지만, 가장 최근 커밋이 9 days ago 였다.
현재 내가 Python 3.8로 개발을 하였고, 해당 버전에 대한 이슈는 없었으므로 이 라이브러리로 도전했다.



### 원래 Swagger는 Spring에서 어떤 식으로 사용하지?
