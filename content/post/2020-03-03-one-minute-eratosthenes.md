---
categories:
- Algorithm
date: "2020-03-03T00:00:00Z"
excerpt: 에라토스테네스의 체는 정말 금방인걸요?
last_modified_at: 2020-03-03TO15:30:00+09:00
tags:
- 에라토스테네스의 체
title: 에라토스테네스의 체가 모야
toc: true
toc_sticky: true
---

나중에 빨리 복습하고 싶어서 정리합니다.

# 목차
- [목차](#목차)
- [출처](#출처)
  - [간단 정리](#간단-정리)
  - [구현](#구현)
    - [비트 마스크를 이용한 최적화 방법?](#비트-마스크를-이용한-최적화-방법)

# 출처
- [에라토스테네스의 체](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)
- [최적화된 에라토스테네스의 체](Eratosthenes' sieve)  

## 간단 정리
![](https://commons.wikimedia.org/wiki/File:Sieve_of_Eratosthenes_animation.gif)

정말 간단 <br>
고려할 포인트
- 1~n 까지의 구간에 대해서 소수를 구하는 것이다
- 1, 2, 3 ... k 까지 차례로 나눠나갈 때 k^2 > n 을 만족하는 k 까지만 구해보면 된다

## 구현 

- 1 ~ n  구간의 n 을 input 받아온다
- n이 0, 1 일 경우 바로 return 한다 (alternative flow)
- **boolean[] 을 n+1 크기**로 만들고 다 true로 초기화 한다
- 0, 1 을 false 처리 한다
- 2 부터 차례로 걸러내기 시작한다
- k^2 > n 을 만족하는 k 까지만 걸러 낸다.

### 비트 마스크를 이용한 최적화 방법?
**실제 코딩테스트에서는 k^2 > n 를 이용한 방법이면 충분하다**고 나와있어서, 따로 정리하지 않았다. 그리고 이것은 이미 수학적으로 증명된 방법이라 마음 놓고 사용해도 된다.

