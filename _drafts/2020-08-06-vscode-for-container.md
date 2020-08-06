---
title:  "vscode를 통해 컨테이너 내부에서 개발하기"
excerpt: "vscode remote development을 통해 컨테이너로 개발 환경을 띄워서 개발하기"


categories:
-  Docker
tags:
-  도커 개발 환경
-  vscode remote development
last_modified_at: 2020-08-06TO20:30:00+09:00
---

### 나의 고민

docker-compose로 개발 환경을 구성하긴 했는데...
컨테이너 들어가서 vim으로 개발해도 되긴 한데,
vscode와 같은 IDE가 아직 익숙한데 어떻게 안되나?

차선책으로 bind mount를 통해 로컬에서 개발하고 있었는데,
로컬에는 라이브러리가 다 깔려있지 않기 때문에 실행하기 전까지는 오류를 알 수가 없다.

앞으로 소개할 vscode 확장 프로그램을 사용하면,
컨테이너 내부에서 개발을 할 수 있고,
컨테이너 내부의 터미널도 vscode 터미널로 바로 사용할 수 있다.

## vscode extension : remote development

