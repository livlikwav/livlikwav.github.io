---
title:  "Java는 Call by Value일까, Call by Reference일까?"
excerpt: "Java의 인자전달방식은 무엇일까?"

categories:
  - Java
tags:
  - Java
  - Algorithm
last_modified_at: 2020-01-20TO20:00:00+09:00
---

# 목차
- [1번째 글](#1번째-글)
- [2번째 글](#2번째-글)
- [3번째 글](#3번째-글)
- [나름의 결론](#나름의-결론)


# 출처
- [자바의 아규먼트 전달 방식](https://brunch.co.kr/@kd4/2)
- [Is Java “pass-by-reference” or “pass-by-value”?](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value)
- [Java 인자 전달 방식: Call by Value or Reference?](http://mussebio.blogspot.com/2012/05/java-call-by-valuereference.html)

# 1번째 글
call by value 
> 값 복사 = 깊은 복사 = deep copy = 객체의 실체값 복사

call by reference 
> 참조 복사 = 얕은 복사 = shallow copy = 객체의 참조값(주소값) 복사

자바는 언제나 'call-by-value'이다.
헷갈릴 수 있는 것은, 말 그대로 value를 넘기기 때문에
* 기본자료형을 인자로 넘기면 값을 넘기고
* 참조자료형을 인자로 넘기면 레퍼런스를 넘긴다.

자바의 자료형은 기본자료형과 참조자료형이 있다.

필자는 다음 작성할 두가지 글을 추천하면서,
더 깊게 공부하는 것을 추천하셨다.

# 2번째 글
StackOverflow 글
### 질문
I always thought Java was  **pass-by-reference**.
However, I've seen a couple of blog posts (for example,  [this blog](http://javadude.com/articles/passbyvalue.htm)) that claim that it isn't.
I don't think I understand the distinction they're making.
What is the explanation?
>나는 자바가 참조복사라고 늘 생각해왔다. 그러나, 나는 내 생각이 틀렸다는 몇몇의 글을 보았다. 나는 그들이 말한것의 차이를 이해할 수 없다. 설명을 부탁한다.

### 댓글들
    I believe that much of the confusion on this issue has to do with the fact that different people have different definitions of the term "reference". People coming from a C++ background assume that "reference" must mean what it meant in C++, people from a C background assume "reference" must be the same as "pointer" in their language, and so on. Whether it's correct to say that Java passes by reference really depends on what's meant by "reference".  – Gravity
> 나는 이러한 혼란이 많은 사람들이 '참조'라는 용어에 대해서 다른 정의를 갖고 있기 때문이라고 생각한다. C++의 배경지식이 있는 사람들은 '참조'가 C++ 내의 참조의 뜻이라고 생각한다, C의 배경지식이 있는 사람들은 '참조'를 '포인터'와 같다고 생각하고, 다른 언어도 마찬가지이다. 
> 그래서, 자바가 참조복사가 맞는지에 대한 질문은 '참조'를 어떻게 정의하느냐에 따라 맞기도 하고 틀리기도 하다.

I try to consistently use the terminology found at the  [Evaluation Strategy](http://en.wikipedia.org/wiki/Evaluation_strategy)  article. It should be noted that, even though the article points out the terms vary greatly by community, it  _stresses that the semantics for  `call-by-value`  and  `call-by-reference`  differ in a very crucial way_. (Personally I prefer to use  _`call-by-object-sharing`_  these days over  _`call-by-value[-of-the-reference]`_, as this describes the semantics at a high-level and does not create a conflict with  _`call-by-value`_, which  _is_  the underlying implementation.) – user166390
> 나는 링크(평가전략 - 위키피디아)에서 찾은 용어를 지속적으로 사용하려 노력해왔다.  이 글에서는 call-by-value와 call-by-reference가 매우 중요하게 다르다고 한다. (나는 요즘 call-by-value, call-by-value of the reference 보다 call-by-object-sharing 이라는 단어를 사용하려고 노력한다, 이 단어는 더 상위 개념의 의미이고, call-by-value라는 단어와 충돌을 일으키지 않는다.

reference 라는 단어 자체의 문제를 지적한 것 같은데, 아직까지는 더 이해를 방해하기만 하니, 답으로 넘어가보자

### 답
Java is always  **pass-by-value**. Unfortunately, when we pass the value of an object, we are passing the  _reference_  to it. This is confusing to beginners.
> 자바는 늘 '값 복사'이다. 불행하게도, 우리가 객체의 값을 넘겨주면, 우리는 그것의 참조를 넘겨주는 것이다. 이것이 초심자에게 혼동이 된다.

It goes like this:
> 이것은 다음 코드로 설명할 수 있다.

```
public static void main(String[] args) {
    Dog aDog = new Dog("Max");
    Dog oldDog = aDog;

    // we pass the object to foo
    foo(aDog);
    // aDog variable is still pointing to the "Max" dog when foo(...) returns
    aDog.getName().equals("Max"); // true
    aDog.getName().equals("Fifi"); // false
    aDog == oldDog; // true
}

public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // change d inside of foo() to point to a new Dog instance "Fifi"
    d = new Dog("Fifi");
    d.getName().equals("Fifi"); // true
}
```

In the example above  `aDog.getName()`  will still return  `"Max"`. The value  `aDog`  within  `main`  is not changed in the function  `foo`  with the  `Dog`  `"Fifi"`  as the object reference is passed by value. If it were passed by reference, then the  `aDog.getName()`  in  `main`  would return  `"Fifi"`  after the call to  `foo`.
> 위의 예제에서  `aDog.getName()`  는 여전히 `"Max"`를 리턴한다. `main`에서의 `aDog`는  함수 `foo`에서 `"Fifi"`로 교체되지 않는다, 객체의 레퍼런스가 값 자체로 복사되기 때문에.

**아직까지는 이해가 안된다. 레퍼런스 자체를 값 복사로 넘겨줬으면 레퍼런스를 넘겨준거 아닌가!!? 더보자**

Likewise:

```
public static void main(String[] args) {
    Dog aDog = new Dog("Max");
    Dog oldDog = aDog;

    foo(aDog);
    // when foo(...) returns, the name of the dog has been changed to "Fifi"
    aDog.getName().equals("Fifi"); // true
    // but it is still the same dog:
    aDog == oldDog; // true
}

public static void foo(Dog d) {
    d.getName().equals("Max"); // true
    // this changes the name of d to be "Fifi"
    d.setName("Fifi");
}
```

In the above example,  `Fifi`  is the dog's name after call to  `foo(aDog)`  because the object's name was set inside of  `foo(...)`. Any operations that  `foo`  performs on  `d`  are such that, for all practical purposes, they are performed on  `aDog`, but it is  **not**  possible to change the value of the variable  `aDog`  itself.

**두 예제의 차이**
`foo()` 내부에서 
* `d = new Dog("Fifi");`
* `d.setName("Fifi");`

**내 이해:**
말그대로 객체의 레퍼런스 자체를 pass-by-value로 보내주기 때문에, 
`foo()` 내에서 새로운 레퍼런스 변수 `Dog d`가 있는거고, 그 d는 `main`에 레퍼런스 변수 `Dog aDog`가 가리키는 객체를 가리킨다.

그래서 `foo()`내의 `Dog d`에 `d = new Dog("Fifi");`를 하면,
`foo()`내의 `Dog d`가 새로운 객체 `Dog("Fifi")`를 가리키는 것이고

`d.setName("Fifi");`를 수행하면 `Dog d`가 가리키는, `Dog aDog`도 가리키고 있는 객체가 메소드를 수행하므로, 다시 `main`절로 나가서 `Dog aDog`가 가리키고 있는 객체의 `getName()`을 수행하면 `"Fifi"`로 바뀌어 있는 것이다.

**밑의 답변들은 읽고 넘겼다. 그림 예제도 있으니 한번씩 훑어 보면 이해에 도움이 될 것이다.**

# 3번째 글

### 사전지식
메서드나 함수의 인자 전달 설명할 때 항상 등장하는 단어
parameter
> formal parameter (형식인자)

argument
> actual-parameter (실인자)

**Syntax와 Semantics란?**
Syntax
> 말 그대로 언어의 구문 규칙

Semantics
> 컴파일러가 구문(Syntax)를 분석한 뒤 해석하여 실제로 동작에 사용되는 명령어를 생산해 내는데 사용되는 지침(모델)이다.

예제)
```
//Case1.
int  primitiveIntVar = 1024;
//Case2.
String whoAreYou = "It's me! Uncle Bob";
```

**두 case의 Syntax는 거의 비슷하다**
> Syntax는 말그대로 언어의 구문 규칙, 작성 문법이므로 하나의 변수에 값을 대입하는 형태를, 두 case 동일하게 띄고 있으므로 거의 비슷하다.

**두 case의 Semantic은 완전히 다르다 **
> case1은 "정수형 변수 primitiveIntVar에 정수 1024를 저장"
> case2는 
> 1. 문자열 객체 "It's me! Uncle Bob" 생성
> 2. String 타입 변수 whoAreYou에 생성된 객체의 레퍼런스를 저장
> 하는 명령어를 만들어 내시오 라는 의미를 가지고 있다.

### 결론
**만약 Java가 call-by-reference 매커니즘을 지원한다면 참조변수 sam 자체의 레퍼런스(주소)를 얻을 수 있는 방법이 있어야 합니다. 그러나 Java는 이 방법을 지원하지 않습니다. 따라서 "참조변수 sam에 저장된 값(다른 객체의 레퍼런스 값)"을 복사하여 formal-parameter p로 넘겨준 call-by-value 매커니즘이 합당해 보입니다.**

- 두 매커니즘의 정리
	-   passing  value of actual-parameter variable : call-by-value
	-   passing  reference of actual-parameter variable : call-by-reference
-   Java의 메서드 인자전달 방식은 call-by-value
	-   value란? 객체에 대한 포인터 값(레퍼런스) 또는 primitive 타입의 값

# 나름의 결론
Java의 메서드 인자전달 방식은 call-by-value이다.

C와 C++의 call-by-reference와의 별개로 생각해야할 점은,
C와 C++에서 말하는 reference와 Java에서 말하는 reference는 다르다.

(내이해)
C와 C++에서 말하는 reference는 기본자료형으로 정확히 주소값, 그 비트값이고,
Java에서 말하는 reference는 참조자료형 변수인 레퍼런스 변수를 말하는 것이다.

이와 같은 문제는, 평가 전략(Evaluation Strategy) 와 관련된 문제이다.
평가전략이란 프로그래밍 언어에서
1. 함수 호출의 argument의 순서를 언제 결정하고
2. 함수에 어떤 종류의 값을 통과시킬지 결정하는 것이다.
[https://ko.wikipedia.org/wiki/평가전략](https://ko.wikipedia.org/wiki/%ED%8F%89%EA%B0%80_%EC%A0%84%EB%9E%B5_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))

### 추신
**제임스 고슬링**
자바를 최초 개발하여 '자바의 아버지'라고 불린다.
가장 영향력 있는 프로그래머들 가운데 한 사람이다.
자바(Java)라는 명칭은 유명한 커피 재배지인 인도네시아 섬 이름인 자바섬에서 따왔다고 한다.
자바 커피를 하루에도 10여잔 씩 마시는 자바 예찬론자 이기도 하다.