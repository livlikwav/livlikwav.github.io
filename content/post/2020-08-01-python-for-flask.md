---
categories:
- Python
date: "2020-08-01T00:00:00Z"
excerpt: 모듈, 패키지, 정적 메소드
last_modified_at: 2020-08-01TO20:30:00+09:00
tags:
- Flask
- Python
title: Flask에 필요한 Python 사용법
toc: true
toc_sticky: true
---

일단 Flask로 개발하기로 했다. 그래서 Top-down 방식으로 Flask 부터 배웠고, Python에 대한 나의 부족함이 드러나기 시작했다.(분명히 배웠었는데 ㅎㅎ)

나는 일단 Flask-sqlalchemy 관련 코드까지 싹 다 app.py에 작성하고 있었다. ORM부터 배워서 바로 개발하다가 스크롤을 내리기 힘들어져서 찾아봤다.

## Python Module

[참고한 링크](https://victorydntmd.tistory.com/242)
당연히 한 파일에 많은 내용이 들어있으면 나중에 유지 보수 하기가 힘들어지고, 의미적으로도 분리가 어렵다. 따라서 **기능별로 모듈 단위를 만드는 모듈화가 필요하다.**

어떤 기능을 구현한 모듈을 만들어놓고, 쓰고자 하는 곳에서 import로 불러오기만 하면 된다.

import로 모듈을 불러올 때 신경 써야 할 부분은 모듈이 존재하는 경로이다. **대부분 모듈은 특정 디렉터리에 모아놓고 관리하기 때문에, 디렉터리를 import하는 방법을 알아야 한다.**

`import MyModule`
같은 디렉터리 내의 MyModule.py를 Import할 수 있다. 다음과 같이 사용해야 한다.
`MyModule.add(10, 20)`
`MyModule.subtract(20, 10)`

`from math import sin, pi`
이와 같이 모듈에서 특정 변수와 메소드만 불러올 수 있다. 또한 **as**를 통해 별칭을 줄 수 있다. 다음과 같이 바로 사용할 수 있다.
`sin(pi/2)`

## Python Package

[참고한 링크](https://wikidocs.net/1418)
**패키지란 모듈을 모아 놓은 단위이다.**
패키지는 관련된 모듈들을 계층적인 디렉터리 구조로 저장하여 관리하기 위함이다.
> 패키지는 도트(.)를 사용하여 파이썬 모듈을 계층적으로 관리할 수 있게 해준다. 예를 들어 모듈 이름이 A.B인 경우에 A는 패키지 이름이 되고, B는 A 패키지의 B 모듈이 된다.

PyCharm같은 파이썬 에디터를 사용하면 패키지 만들면 \_\_init\_\_.py 파일을 자동으로 생성해주나 보다. 나는 VSCode를 쓰고 있어서 그런가 만들어지지는 않았다.

\_\_init\_\_.py 파일은 **패키지를 인식시켜주는 역할을 하는 파일이다. 즉 특정 디렉터리가 패키지로 인식되기 위해서는 init.py파일이 필요하다.**

사실, **python 3.3 부터는 init 파일 없어도 패키지로 인식한다고 한다.** 하지만 하위 버전 호환을 위해 파일을 생성하는 것이 안전한 방법이다.

- project
  - pack1
    - \_\_init\_\_.py
    - MyModule.py
  - pack2
    - \_\_init\_\_.py
    - test.py

와 같은 디렉터리와 파일을 만들자. 이러한 모듈을 import하는 방법은 두가지이다.

`from pack1 import MyModule`
`MyModule.test_echo()`
와 같이 파일이름을 앞에 명시한다. 또는,

`from pack1.MyModule import *`
`test_echo()`
와 같이 디렉터리.모듈파일로 import하면 바로 사용할 수 있다.

패키지 내의 init 파일을 사용하는 방법도 있다.
init 파일의 사용 방법이 좀 특이하다

### from ~ import ~ 주의할 점

[참고링크 : 파이썬 import한 모듈과 패키지를 찾는 과정](https://velog.io/@anrun/python-%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%B4-import%ED%95%9C-%EB%AA%A8%EB%93%88%EA%B3%BC-%ED%8C%A8%ED%82%A4%EC%A7%80%EB%A5%BC-%EC%B0%BE%EB%8A%94-%EA%B3%BC%EC%A0%95)

`from .model import user`와
`from model import user`는 엄연히 다른 것이다!

### init 파일의 용도

- project
  - pack1
    - \_\_init\_\_.py
    - Hello.py
    - MyModule.py

1) **init 파일 내에 \_\_all\_\_ 변수 설정하여 import * 하기**
`__all__ = ['Hello', 'MyModule]`와 같이 내부에 all 변수를 설정해주면,
`from pack1 import *`을 통해서 패키지 내의 정해진 모듈을 한번에 import할 수 있다.

2) **init 파일 내에 from . import 문 나열하기**
pack1 패키지에서 MyModule만 import될 수 있도록 범위를 제한하고 싶다면,
init 파일에서 `from . import MyModule`라고 작성한다.

3) **init 파일 내에 코드를 작성한다 = 패키지에서 바로 메소드를 import 하려면**
`from pack1 import create_app`과 같이 사용하려면, \_\_init\_\_.py에 해당 메소드를 선언하면 된다.

또한 from 에서 relative 한 접근자인 (.)와 (..)을 사용할 수 있다.

## Python staticmethod

[참고한 링크](https://medium.com/@hckcksrl/python-%EC%A0%95%EC%A0%81%EB%A9%94%EC%86%8C%EB%93%9C-staticmethod-%EC%99%80-classmethod-6721b0977372)
데코레이터를 사용한다.

### @staticmethod

인스턴스 메소드와 달리 self라는 인자를 가지고 있지 않다.

### @classmethod

인스턴스 메소드와 달리 self라는 인자 대신 cls라는 인자를 가진다.

### 두 정적 메소드의 공통점 : 인스턴스에서 접근

파이썬에서는 정적메소드임에도 불구하고 인스턴스에서도 접근이 가능하다.

### 두 정적 메소드의 차이점 : 상속

@staticmethod는, **부모 클래스의 클래스 속성 값을 가져온다.**
@classmethod는, **cls 인자를 활용하여 현재 클래스의 클래스 속성을 가져온다.**

### __name__ 변수란

파이썬의 \_\_name\_\_ 변수는 파이썬이 내부적으로 사용하는 특별한 변수 이름이다. 모듈 파일을 직접 실행할 때만 실행되는 코드를 **if \_\_name\_\_ == "\_\_main\_\_":** 조건문에 담는다.