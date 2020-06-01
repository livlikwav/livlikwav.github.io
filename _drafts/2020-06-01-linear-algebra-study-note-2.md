---
title:  "선형대수 공부정리 2편"
excerpt: "내가 이해하기 쉽게 직접 그리면서 정리하는 러너게인 선형대수 강의"


categories:
-   공부
tags:
-   선형대수
last_modified_at: 2020-06-01TO15:30:00+09:00
---

기말고사가 얼마 남지 않았습니다. 과제도 한번 더 나온다고 하니, 미리미리 공부하고 정리를 해둬야 겠습니다. 나중에는 문제를 많이 풀어봐야겠죠.

# 목차

참고한 블로그 : [Learn Again! 러너게인](https://twlab.tistory.com/)
1.  [4강. LU Decomposition(분해)](https://twlab.tistory.com/12category=668741)
2.  [5-1강. 치환행렬(Permutations), 전치(Transposes), 대칭행렬(SymmetricMatrix)](https://twlab.tistory.com/13?category=668741)
3.  [5-2강. 벡터공간(Vector space), 부분공간(Sub spaces)](https://twlabtistory.com/15?category=668741)
4.  [6강. Column space와 영공간(Null space)](https://twlab.tistory.com/17category=668741)
5.  [7강. Null space 계산 알고리즘. Ax=0과 Pivot variable 그리고 Free variable](https://twlab.tistory.com/21?category=668741)
6.  [8강. 선형방정식 Ax = b의 완전해(complete solution)과 Rank](https://twlabtistory.com/22?category=668741)
7.  [9강. 선형 독립(linear independance), Span, 기저(Basis) 그리고 차(Dimension)](https://twlab.tistory.com/24?category=668741)

# 4강. LU Decomposition(분해)

LU Decomposition
= LU Factorization 과 같은 말입니다.

어떤 행렬 A,
하삼각 행렬 L (Lower triangular matrix),
상삼각 행렬 U (Upper triangular matrix)

A를 L과 U의 곱으로 분해하여 나타내는 것입니다.

LU분해는 가우스 소거(Gauss Elimination)에 의한 Elimination 행렬 형태라고 볼 수 있습니다.
때때로, 치환행렬(Permutation matrix)를 포함하기도 합니다.

컴퓨터가 LU분해를 사용할 때
- sparse 형태의 선형 방정식을 계산할 때
- 역행렬(Inverse matrix) 계산
- 행렬식(determinant) 계산

## 행렬 곱셈의 Inverse

LU 분해의 이해를 돕기 위해 행렬 곱셈의 Inverse를 살펴봅니다.

![inversemulti](https://user-images.githubusercontent.com/44190293/83380931-3a279900-a41a-11ea-8dcd-78eb100bcd72.png)

## 행렬 곱셈의 전치 (Transpose)

전치란,
row의 원소들이 column이 되고, column의 원소들이 row의 원소가 되는 것입니다.

A의 역행렬의 전치 = A의 전치 행렬의 역행렬
(단, 이 규칙은 각각의 단일 행렬에 대해서만 적용됩니다.)

## LU Decomposition

### Decomposition 분해란?

Decomposition
-  Factorization과 같은 말입니다.
-  어떤 시스템 혹은 데이터를 표현한 행렬 A를 인수분해한다는 뜻입니다(중고등학교때 인수분해 처럼)
-  어떤 행렬(Matrix)를 여러 행렬들의 곱으로 표현하는 것을 의미합니다.

Decomposition 하는 이유
-  그 방정식의 해를 구하기 위함입니다(중학교때 했던 이유와 같이)
-  **1) 계산의 편리함**
-  **2) 분석적 용이성**
-  결국 계산을 더 편리하게 하고 어려운 문제를 쉽게 풀기 위해,
-  시스템 행렬을 단순화시켜 표현하여 분석을 용이하게 하기 위함입니다.

행렬 분해의 다양한 종류
-  SVD(Singular Vector Decomposition)
-  QR Decomposition
-  LU Decomposition
>  각각 고유의 분해 특성을 가지며, 다양한 문제를 푸는데 사용됩니다.

### LU Decomposition 과정

![ludecompose](https://user-images.githubusercontent.com/44190293/83381868-c2a73900-a41c-11ea-93ec-35413c7c132c.png)

## LDU Decomposition

이 Pivot들만 따로 떼어서 분해하고 싶은 경우입니다.

D는 Diagonal Matrix입니다.
대각 행렬은, 대각선 방향의 원소만 가지고 있는 행렬을 의미합니다.

Pivot들만 따로 떼어 놓은 D 행렬을 U행렬로 부터 분해합니다.

![ldudecompose](https://user-images.githubusercontent.com/44190293/83382498-2da53f80-a41e-11ea-8841-1b9350b9fc4d.png)

## A=LU에서 L의 장점

![Lisbetter](https://user-images.githubusercontent.com/44190293/83383176-8a552a00-a41f-11ea-9a67-7f0f50915dc0.png)

## PA=LU Decomposition

치환행렬 P를 곱해서 PA=LU와 같이 분해를 수행할 수 있습니다.

### 치환행렬의 성질 Permutations

![permutations](https://user-images.githubusercontent.com/44190293/83383744-b58c4900-a420-11ea-905d-21a4c3f78472.png)

**주의할 점**
P_13이나, P_23은 대각 원소들 기준으로 좌우 대칭이지만,
P_13 * P_23과 같이 행 교환 2번 수행한 행렬은 좌우 대칭이 아닙니다.

치환 행렬 = P_12
치환 행렬의 조합 = P

치환 행렬의 조합의 개수는,
결국 결과 행렬인 P가 row 3, row 2, row 1 대상으로 줄세우기를 하면 
6가지 경우의 수가 나오지만

딱 한번의 행교환을 수행하는 P_12와 같은 행렬은 
(3 * 2)/(2 * 1) = 3 가지 밖에 없습니다.

## 선형 시스템(Linear System)의 표현은 유일하지 않다.

선형 방정식을 모아 놓은 것이기 때문에,
어떻게 쌓느냐 순서에 따라(행이 바뀌면) 당연히 다른 표현이지만,
시스템 자체는 같습니다.

위의 개념을 생각했을 때,
**LU Decomposition은 일반적으로 PA=LU와 같이 표현할 수 있습니다.**

# 5-1강. 치환행렬(Permutations), 전치(Transposes), 대칭행렬(SymmetricMatrix)

### MATLAB 에서의 permutation 

1. pivot이 0인지를 체크한다
2. pivot 값이 충분히 큰지를 체크한다

pivot 값이 0에 가깝다면 수치적으로(numerically) 좋지 않다고 합니다. 대수적으로는 이러한 과정이 필요하지 않지만, 수치 정확도(numerical accuracy)가 좋지 않아서 계산 결과가 좋지 않을 수 있습니다. 따라서 **0에 가까운 pivot 연산이 있을 경우 MATLAB은 행 교환 연산을 수행합니다.**

## 치환 행렬의 2가지 편리한 속성

1. **모든 P행렬은 Invertible 하다**(역행렬이 존재하는 단위행렬에서 행만 바꿨으므로 당연합니다.)
2. **P행렬의 역행렬은 전치(Transpose)행렬과 같다**

## 전치(Transpose)의 속성

정방행렬이 아닌 직사각행렬을 전치하면,
row 차원과 column 차원이 뒤바뀝니다.

A_ij > A_ji 로 원소의 값이 바뀝니다 = 전치(Transpose)

## 대칭 행렬(Symmetric Matrix)

**전치를 해서 행렬을 뒤집어도 원래 행렬과 같은 특성을 지닙니다.**

### 대칭 행렬을 구하는 법

![symmtarix](https://user-images.githubusercontent.com/44190293/83385426-313bc500-a424-11ea-997e-40691ab04666.png)

# 5-2강. 벡터공간(Vector space), 부분공간(Sub spaces)

