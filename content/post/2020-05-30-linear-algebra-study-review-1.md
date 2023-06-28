---
categories:
- Study
date: "2020-05-30T00:00:00Z"
excerpt: 배경지식 ~ 3강
last_modified_at: 2020-05-30TO15:30:00+09:00
tags:
- 선형대수
title: 선형대수 - 러너게인 정리
toc: true
toc_sticky: true
---

선형대수를 공부하며 많이 참고한 블로그이다.
내 나름대로 정리하며 공부해보았다.

## 목차

[Learn Again! 러너게인](https://twlab.tistory.com/)

1. [배경지식](https://twlab.tistory.com/3?category=668741)
2. [1강 : The Geomerty of Linear Equations](https://twlab.tistory.com/4?category=668741)
3. [1강-2 : The Geomerty of Linear Equations(2)](https://twlab.tistory.com/6?category=668741)
4. [2강 : 소거법, 후방 대입법 그리고 소거 행렬](https://twlab.tistory.com/8?category=668741)
5. [3강 : 행렬곱셉(Matrix Multiplication), 역행렬(Inverse matrix) 그리고 Gauss-Jordan](https://twlab.tistory.com/10?category=668741)

## 1) 배경지식

해당 블로그 강의는 MIT의 gilbert strang 교수님의 강의를 기반으로 정리했습니다.

선형대수란?

- Linear Algebra
- 선형 방정식을 풀기 위한 방법론

결국 **선형 대수**라는 것은 
**선형성(linearity)을 가지는 대수(algebra)로 이루어진 방정식들의 해를 구하는 방법론, 혹은 학문**을 말합니다.

2x + 3y = 0와 같은 선형 방정식(Linear equation)이 있는데,
여기서 우측의 해 (0) 을 만족시키는 x와 y를 찾아내는 방법을
**선형대수**라고 말합니다.

**선형**이란,
입력에 a라는 영향을 주면 그에 따른 출력 값도, 기존의 출력값에서 a라는 영향을 받은 만큼의 결과 값이 나오는 시스템입니다. 다시 말해 **예측이 가능한 시스템**입니다.

선형성(linearity)의 예시 2가지
![linear1](https://user-images.githubusercontent.com/44190293/82788767-10172980-9ea4-11ea-928f-d386e7038301.png)
![linear2](https://user-images.githubusercontent.com/44190293/82788790-1907fb00-9ea4-11ea-85b5-498800515e8c.png)

입력 부분의 계수 값에 따라서 결과값이 그대로 예측이 가능합니다.

**대수**란?
숫자를 대신하는 것(문자)을 말합니다.

**대수학**이란?
숫자를 대신하는 대수를 이용하여 방정식을 풀고 해를 구하는 것을 말합니다.

선형 대수에서는 이 계수들이 매우 중요한 의미를 갖습니다. 이 계수들을 활용하여 연립방정식의 해를 구하게 될 것입니다.

## 2) 1강 : The Geometry of Linear Equations

선형연립방정식을 행렬로 표현하는 방법
![makematrix](https://user-images.githubusercontent.com/44190293/82788806-1f967280-9ea4-11ea-8c54-b83b99ad8179.png)

이제 알아야할 것은 이 시스템에서 다음이 의미하는 것들입니다.

- Row Picture
  - Row 방향의 방정식을 하나씩 보는 것입니다. 이 방정식이 공간상에서 어떻게 표현되는지, 무엇을 의미하는지 아는 것입니다.
- Column Picture
  - 위 행렬의 계수 행렬에서 column방향의 벡터들을 보고 이것의 의미가 무엇인지, 그리고 공간상에서는 어떻게 표현되는지 이해하는 것입니다.
- Matrix Form
  - 이러한 Row와 Col picture들로 이루어진 Matrix에 대해 그 의미를 이해하는 것입니다. 위 식에서 A에 해당합니다.

## Row picture

한 번에 하나의 **row 방향의 방정식을 따져 보는 것**을 의미합니다. 선형대수에서 이러한 row 방향의 하나의 방정식은 좌표 공간상에서 직선이나 평면 등으로 표현 됩니다. 

예를 들어,
2x2 행렬에서 Row picture의 해는 **해당 직선들이 만나는 교점**입니다.

> 행렬에서 각 Row에 해당하는 방정식을 한 번에 하나씩 보는 것이 Row picture이고, 각 Row 방정식들의 교점을 찾는 것이 목표이고, 그 교점이 그 시스템의 해입니다.

## Column picture

![colpicture](https://user-images.githubusercontent.com/44190293/82788711-ef4ed400-9ea3-11ea-9005-0613d81bbc35.png)

Column picture는 계수 행렬에서 **동일한 변수가 곱해지는 계수들을 묶어서 정리한 것**입니다. 결과는 col vector들과 각 변수의 곱의 조합으로 표현되어 집니다.

이와 같은 **(벡터 * 상수)의 Summation을 선형 결합(Linear Combination)**이라고 합니다.

선형 결합은,

1. 선형대수에서 가장 근본적이며 핵심적인 연산입니다.
2. 주어진 벡터들에 어떤 상수 x와 y가 곱해져야 우변의 벡터 값이 나오는가? 를 묻습니다.
3. 즉 우항의 벡터를 만족시키기 위한 적절한 선형 결합은 무엇인가? 를 묻습니다.
4. 이것이 곧 해이고 핵심입니다.

계수 행렬의 각 column은 공간상에서 벡터로 표현됩니다. 이 시스템에서 **해를 찾는 과정은, 좌항의 적절한 선형 결합을 찾는 것**입니다.
(Row picture에서 각 row의 방정식이 공간상에서 직선이나 평면등으로 표현되는것과는 비교가 됩니다. 또한 Row picture에서의 해를 찾기 위해서는 선형결합이 아닌 두 방정식의 공간상의 교점을 생각해야 합니다)

## 요약

![col,rowpic](https://user-images.githubusercontent.com/44190293/82788687-e3631200-9ea3-11ea-8c5d-9346b39b842b.png)

- Row picture나 col picture나 어짜피 똑같은 시스템 A를 보는 것입니다( 따라서 해는 같습니다.)
- **Row : 문제를 직선이나 평면등의 방정식으로 보는것**
- **Col : 문제를 벡터들의 선형 결합으로 보는것**

## 1강-2 : The Geometry of Linear Equations(2)

그 전의 예제는 2x2 행렬이었지만, 이게 3x3 행렬일 경우에 Row picture와 Column picture의 차이점을 더욱 극명하게 볼 수 있습니다.

Ax = b

- 어떤 시스템을 표현하는 Matrix form A
- 미지수 벡터 x
- A와 x를 곱하여 만들어지는 b

### 이때 미지수 벡터 x를 시스템 행렬 A에 어떠한 방법으로 곱할것인가?

- Row picture
  - **내적(Dot product)**
  - **방정식 하나하나마다 보는것 = 공간상에서 어떤 형태로 나타냄**
  - 3차원 공간상에서 평면으로 표현됩니다.
  - 세 평면의 교점, 교선을 바로 찾는 것이 어려움
  - **dim이 늘어날 수록 더 한눈에 파악하기가 어려움**
- Column picture
  - **선형결합(Linear Combination)**
  - **3차원 벡터들의 선형결합으로 보는것** 
  - 힘들게 평면의 교점을 찾아 구하지 않아도, 선형결합으로 보면 해를 구하기 더 쉽다.

Column picture, 즉 선형결합으로 주어진 식을 볼때, **중요한 2가지 질문**을 할 수 있습니다.

1. Can I solve Ax = b for every b?
2. Do the linear combinations of the columns fill 3-D space?
이 두 질문은 사실 같은 것을 물어보는 것입니다.
다시 말하자면, 시스템 A에서 좌변의 선형결합으로 공간상의 모든 벡터(혹은 점)을 만들어낼 수 있는가?

그렇다는 것은, A matrix는

- non-singular matrix이며,
- invertible matrix이다.
- 이는, A의 col picture의 벡터들이 서로 다른 평면에 존재하기 때문이다.

### Rank란, 어떤 시스템에서 선형 독립(Linearly independant)한 Row vector 혹은 Col vector의 개수를 의미합니다

## 2강 : 소거법, 후방 대입법 그리고 소거 행렬

주제 : 시스템 A의 해를 구하기 위한 방법들을 배웁니다.

1. Elimination(소거법)
   - Success
   - Failure
2. Back-substitution(후방 대입법)
3. Elimination matrices(소거 행렬)
4. Matrix multiplication(행렬 곱)

### 소거법(Elimination)이란, 시스템의 해를 구하는 방법입니다.

주어진 어떤 선형 시스템 A에 대한 해를 구하는 방법이다. 선대를 다루는 모든 SW는 해를 구할 때 이 Elimination 방법을 사용합니다.

### 후방대입법(Back-substitution)은, 소거법을 적용한 이후 해의 실제 값을 구하기 위해 사용합니다.

### 소거행렬(Elimination matrices)은 소거과정을 행렬형태로 표현한 것입니다.

컴퓨터에서 선형대수연산을 수행하기 위해 소거과정이 어떤 식으로 진행되는지를 행렬로 표현한 것입니다. 행렬로 표현하여 행렬연산으로 수행됩니다.

## 소거법 : success case

![eliminationprocess](https://user-images.githubusercontent.com/44190293/83322664-9bbdfb00-a294-11ea-8a8d-b9220bf6192f.png)

### A 행렬 >>>(Elimination)>>> U행렬 (상삼각행렬, Upper triagular matrix)

소거법의 최종 목표는 시스템행렬 A를 u로 만드는 것입니다. 중요한 것은 0인 원소는 pivot이 될 수 없다는 것입니다.

## 소거법 : failure case

pivot이 0이기 때문에 소거가 불가능한 경우 우리는 **Row exchange**를 통해 소거가 가능하도록 만들 수 있습니다. 다만 이 경우에도 **exchange할 0이 아닌 pivot column이 있어야 가능합니다**. 만약 다음 pivot column이 다 0이면 그냥 실패입니다.

failure : 소거 과정에서 pivot이 0인 경우 발생

- 극복이 가능한 temporary failure
  - 다음 방정식 중 pivot 라인의 원소가 0이 아닌 경우가 있을때
  - 결국, Row exchange가 가능할 때
- 극복이 불가능한 complete failure
  - pivot column의 원소가 다 0일 경우
  - 결국, Row exchange가 불가능할 때

## 후방대입법(Back-substitution)

A를 소거법을 통해 U로 만든 이후에, 실제 해를 구하기 위한 과정입니다.

## Augmented matrix

![augmentedmatrix](https://user-images.githubusercontent.com/44190293/83322864-e8ee9c80-a295-11ea-87a5-a5c89c376522.png)

## 후방대입법

![backsubstitution](https://user-images.githubusercontent.com/44190293/83323000-b002f780-a296-11ea-94f1-f3c793b6fc60.png)

## column vector의 linear combination

![right_colpicture](https://user-images.githubusercontent.com/44190293/83323204-1e948500-a298-11ea-89c1-d69f469755b3.png)

## row vector의 linear combination

![left_rowpicture](https://user-images.githubusercontent.com/44190293/83323252-62878a00-a298-11ea-9f4f-972f38a08798.png)

## elimination matrix, permutation matrix

![rowveclinearcomb](https://user-images.githubusercontent.com/44190293/83323323-f22d3880-a298-11ea-9582-f0e750cfb4b1.png)

### 행렬 곱셈의 법칙

1. **교환법칙(Communication Law)은 성립하지 않는다.**
2. **결합법칙(Associative Law)는 성립한다.**

> Elimination matrix를 차례차례 옆에 쌓아야하는 이유!

## 3강 : 행렬곱셉(Matrix Multiplication), 역행렬(Inverse matrix) 그리고 Gauss-Jordan

### 행렬 곱셈의 4가지 관점

1. row * column
   1. 벡터의 내적(dot product)
   2. 가장 일반적인 방법.
   3. 고등학교때 배웠던 방법
2. column-wise
   1. A * B = C일때,
   2. B의 col vector마다 A matrix 와 column vector linear combination을 수행해서 한 column씩 C에 붙인다.
   3. **C의 column들은 A의 column들의 조합이다**
3. row-wise
   1. A의 row vector마다 B matrix 와 row vector linear combination을 수행해서 한 row씩 C에 쌓는다.
   2. **C의 row들은 B의 row들의 조합이다**
4. column * row
   1. row * colum의 형태에서는 곱셈의 결과가 단 하나의 값(scalar)로 나왔다.
   2. 이는 순서가 반대이다.
   3. column x row = **( n, 1) x (1, m)** 이므로 **output = (n, m)**이 나온다 연산마다!
   4. column x row 의 결과 행렬은 **rank가 1인 행렬이다.** (rank는 linearly independent한 row or column의 수, 이를 잘 기억해 놓자)
5. Block Multiplication
큰 행렬 하나를 Block 단위로 분할해서 똑같이 행렬 곱셈을 적용해도 같은 결과가 나온다.
![blockmulti](https://user-images.githubusercontent.com/44190293/83324195-7930df80-a29e-11ea-8750-0e33ed179763.png)

## 역행렬(Inverse Matrix)

역행렬이 존재한다

- Invertible 하다
- nonsingular 하다

행렬 A에 역행렬을 곱해주면 그 결과는 단위행렬(identity matrix)가 됩니다.
**정방행렬일 경우** 역행렬은 왼쪽에 곱해줘도, 오른쪽에 곱해줘도 동일하게 결과는 단위행렬입니다.
**일반적인 행렬일 경우**는 역행렬의 위치에 따라 결과가 달라질 수 있습니다.

### 역행렬이 존재하지 않는다

- =  non-invertible 하다
- =  singular case 이다
- A의 행렬식이 0이 된다(1/(ad-bc))
- **행렬 A의 각 column들이 같은 line 상에 위치한다.**
- **행렬 A는 2x2 행렬이지만, rank는 1이다.**
- **행렬 A의 선형독립(linearly independent)인 차원의 개수가 A의 차원보다 작다**, 따라서 특이행렬이다.
- 행렬 A는 2차원이 아닌 오직 line으로만 표현이 가능하다.
- 이를 확인하는 방법으로 **각 column을 정규화해서 같은지 비교해볼 수 있다.**

하지만 역행렬이 존재하지 않는 가장 큰 이유는...

### 만약 Ax=0을 만족하는 벡터 x를 찾을 수 있다면, 그 행렬은 역행렬이 존재하지 않는다

> **(이때 A는 정방행렬, x는 0이 아닌 벡터)**

### 시스템 A가 어떤 벡터 x를 0으로 보냈다. 이럴 경우, 이렇게 0으로 보낸 x를 다시 원래의 위치로 돌아오게끔 하는 시스템이 존재하는가?

선형대수에서의 연산은 선형 결합, 즉 변수에 어떤 계수들을 곱하고 더해서 계산이 되는 것입니다. 애초에 변수 자체가 0이 되어버렸으면 어떤 계수들을 곱해도 이를 복원시킬 방법이 없는 것입니다.

## Gauss-Jordan idea : 역행렬을 구하는 방법

행렬 A에 역행렬을 곱하면 그 결과가 단위행렬 I가 되어야함을 이용해서 구해냅니다.
**정방행렬에 관한 내용!, 직사각 행렬(Rectangular Matrix)은 pseudo inverse라는 방법을 이용해 계산해야 합니다.**

![gaussjordan](https://user-images.githubusercontent.com/44190293/83324646-c5c9ea00-a2a1-11ea-8f3f-05cde2b0915f.png)

### 이와 같은 과정을 나타내는 제거행렬 E(Elimination Matrix)는 결국 A의 역행렬 입니다.
