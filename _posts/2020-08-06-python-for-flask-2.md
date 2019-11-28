---
title:  "Flask에 필요한 Python 사용법 2"
excerpt: "Decorator, Docstring, 접근제어자, @property"
toc: true
toc_sticky: true

categories:
-  Python
tags:
-  Flask
-  Python
last_modified_at: 2020-08-06TO20:30:00+09:00
---

## decorator

[참고한 글](https://bluese05.tistory.com/30)
[참고한 글2](http://abh0518.net/tok/?p=604)

```python
@decorator
def foo():
    print "hello world"
```

Github에서 Python 코드들을 보다보면 많이 볼 수 있는 골뱅이 @...
꽤 편리한 놈이다.

>decorator를 한마디로 얘기하자면, 대상 함수를 wrapping 하고, 이 wrapping 된 함수의 앞뒤에 추가적으로 꾸며질 구문 들을 정의해서 손쉽게 재사용 가능하게 해주는 것이다.

데코레이터는 유치하게 생각하면 **기존 메소드에 달아서 '데코'를 해주는 것이다.**
여러 함수에 반복적으로 추가하고 싶은 구문이 있으면,
데코레이터로 빼놓고 필요한 메소드마다 데코레이터를 붙이는 것이다.

### 데코레이터 선언 방법

1>함수로 선언한다

```python
def foo(func):
    def foo(*args, **kwargs):
        print("wow"):
        result = func(*args, **kwargs)
        print("wow"):
        return result
    return foo

@foo
def bar(x, y):
    print(x + y)
    return x + y

bar(1, 2)
# wow
# 3
# wow
```

2>클래스로 선언한다

```python
class foo:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("wow")
        result = self.func(*args, **kwargs)
        print("wow")
        return result

@foo
def bar(x, y):
    print(x + y)
    return x + y

bar(1, 2)
# wow
# 3
# wow
```

### 파라미터를 가지는 데코레이터

데코레이터에도 파라미터를 전달하고 싶을 수 있다.
이럴땐 wrapper 함수를 다시 감싸주면 된다.

1>함수식 선언

```python
def foo_with_param(param):
    def bar(func):
        def foo(*args, **kwargs):
            print(param)
            print("wow")
            result = func(*args, **kwargs)
            print(param)
            print("wow")
            return result
        return bar

@foo_with_param("hey, param")
bar(x, y):
    print(x + y)
    return x + y

bar(1, 2)
# hey, param
# wow
# 3
# wow
# hey, param
```

2>클래스식 선언

```python
class foo_with_param
    def __init__(self, param):
        self.param = param
    def __call__(self, func):
        def foo(*args, **kwargs)
            print(self.param)
            print("wow")
            result = self.func(*args, **kwargs)
            print("wow")
            print(self.param)
            return result

@foo_with_param("hey, param")
bar(x, y):
    print(x + y)
    return x + y

bar(1, 2)
# hey, param
# wow
# 3
# wow
# hey, param
```

### decorator와 __doc__같이 사용하기

모든 데코레이터에 **@wraps를 달아준다.**
참고한 블로그 글에 따르면...
>대충 소스 보니 func의 __doc__같은 meta 정보를 wrapper에 복사해 넣는거 같은데 확실한건 아님.

예시

```python
def foo(func):
    @wraps(func)
    def bar(*args, **kwargs):
        # loren ipsum ...
```

## Docstring

[참고한 글](https://wikidocs.net/16050)
Boilerplate를 참고하다가 보면,
한 줄 짜리 주석인데 왜 #을 안쓰고 '''를 썼지? 하고 있었다.

이 좋은걸 몰랐다니!
docstring을 작성하면, **Class.\_\_doc\_\_**이런식으로 바로 접근할 수 있다.
**문서화에서 큰 강점을 갖는 것이다.**

- 모듈, 함수, 클래스, 메소드 다 가능하다.
- 정의의 첫 번째 명령문으로 문자열 정의하면 된다.
- [Docstring coding convention](https://www.python.org/dev/peps/pep-0257/)

예시)

```python
'''
    ~~~ 하는 모듈입니다.
Usage:
    python foobar.py
'''

class Foo:
'''
~~~한 클래스입니다.
Usage:
    foo = Foo()
'''

    def bar(param):
        '''
        ~~~한 ~~~를 하는 함수입니다.
        param Integer
        return Integer|String (T|F)
        '''

help(bar)
# ~~~한 ~~~를 하는 함수입니다.
# :param: Integer
# :return: Integer|String (T|F)

bar.__doc__
# ~~~한 ~~~를 하는 함수입니다.
# :param: Integer
# :return: Integer|String (T|F)
```

## 파이썬 접근 제어자 : Python access modifier

[참고한 글](https://medium.com/@hckcksrl/python-property-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-89eb0f0e2e56)
접근제어자에는 4가지 종류가 있다.

- public
- private
- protected
- default

파이썬은 다른 언어와 달리,
접근 제어자가 없고 작명법으로 접근을 제어해야 한다.

- public : 아무 밑줄(_)이 없다.
- private : 앞에 2개의 밑줄(__) 적용
- protected : 앞에 1개의 밑줄(_) 적용

ex)

```python
class User:
    __secret = "76kg"
    _height = "180cm"
    name = "James"
```

## Python @property

JAVA에서 private 멤버에 접근하기 위해서는,
각각 getValue(), setValue()와 같은 메소드를 직접 만들어준다.

Python에서도 이렇게 직접 get, set 메소드를 만들어 줄 수 있지만,
더 **Pythonic한 방법은 @property 데코레이터를 사용하는 것이다.**

ex)

```python
class User:
    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, name):
        self.__name = name

# test code
user = User()
user.name = 'james'
print(user.name)
```

getter의 역할은 @property가 한다.
setter의 역할은 @field.setter가 한다.
property가 먼저 선언되어야 한다.
