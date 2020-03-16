---
title:  "1분 복습 : BFS, DFS"
excerpt: "SW 마에스트로 코딩테스트를 준비하기 위해, BFS, DFS부터 복습을 해보겠습니다. 1분안에 다시 읽고 복습할 수 있게 정리하겠습니다."

categories:
  - 1분복습
tags:
  - 1분복습
  - PS
last_modified_at: 2020-02-28TO17:30:00+09:00
---

내가 나중에 복습하고 싶어서 정리하는 시리즈.

# 목차
- [생각의 흐름](#생각의-흐름)
- [그래프 탐색의 공통점](#그래프-탐색의-공통점)
- [핵심](#핵심)
- [JAVA는?](#JAVA는?)
- [혹시나 해서](#혹시나-해서)

# 출처
- [너비 우선 탐색(BFS)이란](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)
- [너비 우선 탐색 - wikipedia](https://ko.wikipedia.org/wiki/%EB%84%88%EB%B9%84_%EC%9A%B0%EC%84%A0_%ED%83%90%EC%83%89)
- [BFS - 나무위키](https://namu.wiki/w/BFS)
- [깊이 우선 탐색(DFS)이란](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)

# 생각의 흐름

보통 정의를 까먹지는 않는다. <br>
장점, 단점은 정의로 유추가 가능하다<br>
### 구현 방법, 자료 구조가 헷갈릴 뿐.
**+인접 행렬, 인접 리스트**<br>
**JAVA에서 뭐 사용해서 하더라**

# 그래프 탐색의 공통점

그래프 탐색의 경우 **어떤 노드를 방문했었는지 여부를 반드시 검사해야 한다**.

![image](https://namu.wiki/w/%ED%8C%8C%EC%9D%BC:external/blog.hackerearth.com/dfsbfs_animation_final.gif)

자료구조를 사용할 때, visited set( closed_set )이 없으면 무한루프에 빠질것이다.

# 핵심
### BFS
- 구현 방법 : (대표) **자료구조 Queue**를 사용한다
- 그래프 표현 : 인접 행렬, 인접 리스트
- 
**BFS의 시간 복잡도**
- 인접 리스트 : O(N)
- 인접 행렬 : O(N^2)
- Sparse Graph의 경우 인접 행렬보다 인접 리스트가 유리<br>(당연하게도, 탐색 횟수가 적을 것이기 때문)

### DFS
- 구현 : 순환 알고리즘의 형태
- 구현 방법 : **1) 순환 호출 이용 (재귀 호출)**
- 구현 방법 : 2) **자료구조 Stack**을 사용한다
- 그래프 표현 : 인접 행렬, 인접 리스트

**DFS의 시간 복잡도**
- (정점의 수 :N, 간선의 수: E)
- 인접 리스트 : O(N)
- 인접 행렬 : O(N^2)
- Sparse Graph의 경우 인접 행렬보다 인접 리스트가 유리<br>(당연하게도, 탐색 횟수가 적을 것이기 때문)

# JAVA는?
![image](https://mblogthumb-phinf.pstatic.net/MjAxNjEyMDRfMTc1/MDAxNDgwODU5MjM1OTYx.HKMtAuC2H4yk0ug_53tHElYJd9Mq9B47_2xjeXhF2cIg.0yrzwvt-8FCxecm_MBQTVzK6vWklJ_7YxXDwlYrl0wUg.PNG.writer0713/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2016-12-03_%EC%98%A4%EC%A0%84_12.29.17.png?type=w2)

`Iterator <string> itr = list.iterator();
//모든 컬렉션 안에는 iterator() 메서드가 있다
//hasNext()
//next()
`

`java.util.LinkedList<E>`
> import java.util.*; 로 보통 사용
> 인접리스트 = 이중 linkedlist

`
class Graph{
   private int V;
   private LinkedList<Integer> adj[];
`
# 혹시나 해서
## DFS
### 목표
- 모든 노드를 방문하고자 하는 경우

### 비교
- DFS가 BFS에 비해서 단순 검색 속도 자체는 느리다
- DFS가 BFS보다 좀 더 간단하다.

## BFS

### BFS = Breadth-First Search = 너비 우선 탐색

> 위키피디아

![](https://commons.wikimedia.org/wiki/File:Animated_BFS.gif)

### **장점**
-   출발노드에서 목표노드까지의 최단 길이 경로를 보장한다.

### **단점**
-   경로가 매우 길 경우에는 탐색 가지가 급격히 증가함에 따라 보다 많은 기억 공간을 필요로 하게 된다.
-   해가 존재하지 않는다면 유한 그래프(finite graph)의 경우에는 모든 그래프를 탐색한 후에 실패로 끝난다.
-   무한 그래프(infinite graph)의 경우에는 결코 해를 찾지도 못하고, 끝내지도 못한다.

깊게 탐색하기 전에 넓게 탐색하는 것

### **목적**
- 두 노드 사이의 최단 경로 찾고 싶을 때
- 임의의 경로를 찾고 싶을 때
BFS가 DFS보다 좀 더 복잡하다

### **특징**
- BFS는 **재귀적으로 동작하지 않는다.**
- (DFS는 재귀적으로 동작한다)


