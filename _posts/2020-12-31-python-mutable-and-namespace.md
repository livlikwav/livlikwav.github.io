---
title:  "Python 전역변수, 지역변수 그리고 함수 제대로 사용하기"
excerpt: "namespace, mutable, call by reference과의 삽질 기록"
toc: true
toc_sticky: true

categories:
-  Python
tags:
-  Python namespace
-  Python mutable
-  Python call by reference
last_modified_at: 2020-12-31TO00:10:00+09:00
---

## 도입

늘 그렇듯, 알고리즘 문제를 python으로 풀고 있었는데,  
기본적인 전역변수, 지역변수를 다루는 과정에서 의문이 있었다.  

2-d list를 다루는 dfs 문제였는데,
int는 함수 내에서 global을 사용해서 수정하고,
지도 정보를 담은 2-d list는 global을 사용하지 않고 수정하는 것이다.
> 왜? list는 global 안 쓰고 수정 가능하지?

검색도 열심히 해보고 나름 실험도 해봤다.

## 본론

다음 5가지 기본 개념이 중요했다.

1. Python의 모든 것은 객체다.
2. Python function parameter
3. Python namespace
4. Python immutable/mutable object
5. Python call by reference

### Python의 모든 것은 객체다

`x = 3`  
`y = 'string'`  
여기서 3과 'string'은 둘다 객체다.

### Python function parameter

Python **함수의 파라미터를 통해 변수를 입력**받는 순간,  
해당 파라미터 이름의 **지역 변수**를 할당하는 것이다.

```python
x = 1

def get_x(x: int) -> None:
    print(locals())
    print(globals())
# local에도 x가 있고, global에도 x가 있다
```

### Python namespace

이름 공간이란, 특정 변수 이름이 효력을 갖는 범위를 말한다.  
Python에는 크게 4가지 namespace가 있고, 참조 우선순위는 다음과 같다.  

1. Local
2. Enclosed
3. Global
4. Built-in

특정 변수 명을 호출하면, 위와 같은 우선순위로 해당 이름의 변수를 찾는다.

### Python immutable/mutable object

Python은 크게 2가지 종류의 객체가 있다.

- immutable
  - bool
  - int
  - float
  - str
  - tuple
- mutable
  - list
  - dict
  - set

immutable은 똑같은 값의 두 변수를 선언하면,  
두 변수가 같은 객체를 가리킨다.

immutable은 = 연산자를 사용하여 **값을 변경**하려 할 때마다,  
**새로운 객체를 생성해서 재할당**한다.  

**가장 큰 차이점**은,  
mutable은 indexing, slicing등으로,  
재할당하지 않고 값을 변경할 수 있다.

mutable는 똑같은 값의 두 변수를 선언하면,  
두 변수가 다른 객체를 가리킨다.  
(이는 mutable이라서 언제든 바뀔 수 있어서 그런 것 같다.)

그래서, 이 글에서 가장 중요한 점은 다음 내용인 ...

### Python call by reference

Python에서 함수에 파라미터로 객체를 넘기게 되면(parameter passing),  
해당 local 변수가 넘겨준 global 변수가 가리키는 객체를 **그대로 함께 가리킨다.**  

따라서,
mutable을 받았을 경우에,  
새로운 객체를 재할당하려는 것이 아닌 수정만 하려고 하면,  
**indexing이나 slicing등으로 변경**할 수 있는 것이다.

하지만,
**mutable도 재할당하려면 global을 사용**해야한다.

## 결론

```python
immutable = 1
mutable = [1, 2, 3]

def func1():
    mutable[0] = 1
    # indexing을 통한 변경. 재할당 x
    # global 변수 mutable만을 변경함.
    # local 변수 선언 x

def func2(mutable):
    mutable[0] = 1
    # global 변수 mutable 넘겨줄 경우
    # local과 global이 둘다 동일한 객체를 가리키므로,
    # 두 변수 모두 수정됨.
func2(mutable)

def func3():
    mutable = [7, 7, 7]
    # global 변수 수정 x
    # 새로운 local 변수 mutable 생성함.
    # global 변수에 재할당을 위해서는 global 키워드 사용해야함
```

> 이 정도만 이해하면, 앞으로는 잘 쓸 수 있지 않을까 싶다.

### 삽질의 기록

코드를 따로 정리하지 않아서 **보는 것이 의미없을 것이다.**  
다만, 직접 이렇게 해본게 뿌듯해서 나를 위해 남긴다...ㅎ  

```python
immutable = 1
mutable = [1, 1, 1]

# locals, globals 실험

def print1():
    print('print1', immutable)
    print('print1', mutable)
    print('locals', locals())
    print('globals', globals())

def print2():
    immutable = 2
    mutable = [2, 2, 2]
    print('print2', immutable)
    print('print2', mutable)
    print('locals', locals())
    print('globals', globals())

def print3():
    global immutable
    global mutable
    immutable = 3
    mutable = [3, 3, 3]
    print('print3', immutable)
    print('print3', mutable)
    print('locals', locals())
    print('globals', globals())

# call by reference 실험

def print4(immutable, mutable):
    print('print4', immutable)
    print('print4', mutable)
    print('locals', locals())
    print('globals', globals())

def print5(immutable, mutable):
    immutable = 2
    mutable = [2, 2, 2]
    print('print5', immutable)
    print('print5', mutable)
    print('locals', locals())
    print('globals', globals())

def print5_2(immutable, mutable):
    immutable = 2
    mutable[0] = 2
    print('print5_2', immutable)
    print('print5_2', mutable)
    print('locals', locals())
    print('globals', globals())

def print5_3():
    immutable = 2
    mutable[0] = 2
    print('print5_3', immutable)
    print('print5_3', mutable)
    print('locals', locals())
    print('globals', globals())

def print6(immutable, mutable):
    # global immutable # "immutable" is assigned before global declarationPylance
    # global mutable # "mutable" is assigned before global declarationPylance
    # SyntaxError: name 'immutable' is parameter and global
    # SyntaxError: name 'mutable' is parameter and global
    immutable = 3
    mutable = [3, 3, 3]
    print('print6', immutable)
    print('print6', mutable)
    print('locals', locals())
    print('globals', globals())

# global 2-d list 실험
def print7():
    mutable2 = [1, 1, 1]
    print('print7', mutable2)
    print('locals', locals())
    print('globals', globals())

def print8():
    mutable2[0][0] = 2
    print('print8', mutable2)
    print('locals', locals())
    print('globals', globals())

def print9():
    global mutable2
    mutable2[0][0] = 2
    print('print9', mutable2)
    print('locals', locals())
    print('globals', globals())

def print10(mutable2):
    mutable2 = [1, 1, 1]
    print('print10', mutable2)
    print('locals', locals())
    print('globals', globals())

def print11(mutable2):
    mutable2[0][0] = 2
    print('print11', mutable2)
    print('locals', locals())
    print('globals', globals())

def print12(mutable2):
    mutable2[0][0] = 3
    print('print12', mutable2)
    print('locals', locals())
    print('globals', globals())
    mutable2 = [3, 3, 3]
    print('print12', mutable2)
    print('locals', locals())
    print('globals', globals())
    mutable2[0] = 7
    print('print12', mutable2)
    print('locals', locals())
    print('globals', globals())

def print13(mutable2):
    print('mutable2_print13_id', id(mutable2))
    mutable2[0][0] = 3
    print('mutable2_print13_id', id(mutable2))
    print('print13', mutable2)
    print('locals', locals())
    print('globals', globals())
    mutable2 = [3, 3, 3]
    print('mutable2_print13_id', id(mutable2))
    print('print13', mutable2)
    print('locals', locals())
    print('globals', globals())

# locals, globals 실험
print1()
print2()
print3()
# call by reference 실험
# 초기화
immutable = 1
mutable = [1, 1, 1]
# 시작
print4(immutable, mutable)
print5(immutable, mutable)
print5_2(immutable, mutable)
print5_3()
# print6(immutable, mutable)

# global 2-d list 실험
# 초기화
mutable2 = [[1, 1], [1, 1], [1, 1]]
# 시작
print7()
print8()
print9()
# 초기화
mutable2 = [[1, 1], [1, 1], [1, 1]]
# 시작
print10(mutable2)
print11(mutable2)
print12(mutable2)
print('mutable2_global_past_id', id(mutable2))
print13(mutable2)
print('mutable2_global_future_id', id(mutable2))

# mutable 실험

list1 = [1, 2]
list2 = [1, 2]
list3 = list1

print(id(list1))
print(id(list2))
print(id(list3))

# 같은 객체 가리키고 변화를 줘도 달라지지 않음
list3[0] = 3
print(id(list1))
print(id(list3))

# immutable 실험

int1 = 1
int2 = 1
print(id(int1))
print(id(int2))
# 같은 객체 가리킴 (immutable)

# mutable 과 함수 실험

mut1 = [1, 2, 3]

def get_mut1(mut1):
    print(id(mut1))

def get_mut2(mut1):
    print(id(mut1))

print(id(mut1))
get_mut1(mut1)
get_mut1(mut1)
get_mut2(mut1)

# immutable 과 함수 실험

immut1 = 1

def get_immut1(immut1):
    print(id(immut1))

print(id(immut1))
get_immut1(immut1)
```