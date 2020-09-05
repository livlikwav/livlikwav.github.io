---
title:  "Flask-restful 라이브러리에 Swagger 사용하기"
excerpt: "OpenAPI 기반으로 자동으로 REST API 문서화를 도와주는 Swagger를 Flask에 적용해봅시다."
toc: true
toc_sticky: true

categories:
-  Flask
tags:
-  Swagger
last_modified_at: 2020-09-05TO20:30:00+09:00
---

### 회고

지금까지 Flask로 REST API를 개발하고 있었다.
Swagger가 Spring에서만 쓰인다는 얘기를 듣고,
Swagger UI Editor로 OpenAPI 3.0으로 REST API 설계를 하고,
개발을 한 후, POSTMAN으로 테스트를 수행했다.
이후 문서화는 POSTMAN으로 만들었다.

하지만 역시 나는 초보다.
설계한대로 개발이 이뤄지지 않고, 설계를 수정하게 된다.
API 문서를 POSTMAN 기반으로 작성하고 있지만, 업데이트가 잘 안되는 문제가 있어서
결국에는 Swagger를 사용하기 위해 찾아봤다.

### Flask-restplus library

Flask에서의 REST API 개발을 돕기 위한 라이브러리로 크게 2가지가 있는 것 같다.
Flask-restful과 Flask-restplus.
나는 restful이 코드가 간결해보여서 택했는데, restful은 swagger를 기본적으로 지원해주지는 않았다.
restplus는 지원해주는 것 같았다.

### Flask-restful to Swagger

그렇다면 Flask-restful에서 Swagger를 사용하기 위한 라이브러리는 없을까?
물론 있긴 했다. (Star 수 세자리수 대)
