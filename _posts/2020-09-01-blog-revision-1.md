---
title:  "블로그 개선하기 #1 Minimal mistakes customizing"
excerpt: "폰트 크기 변경, favicon 추가, 작성 일자, 그리고 하이퍼링크 밑줄 없앰"
toc: true
toc_sticky: true

categories:
-  Etc
tags:
-  Jekyll
-  Minimal mistakes
last_modified_at: 2020-09-01TO20:30:00+09:00
---

## 꼭 책상에만 앉으면 딴 짓이 하고 싶다

공부하고 있던 Flutter를 마저 하려고 책상에 앉았다.
저녁도 방금 먹었고, 요즘은 밖에 나가지도 않는다.
시간이 많다..?
내 세련되지 못한 블로그가 눈에 들어왔다.
이런건 역시 날을 잡기보다는 시간이 남을때 딴 짓으로 해야지!

## 현재의 문제

개선에 앞서 현재 문제를 정의했다.

1. Color가 마음에 들지 않는다.
   1. 기본 Skin을 사용하고 있는데, 더 내 마음대로 수정하고 싶다.
2. 폰트 크기가 너무 크다.
3. 포스트 제목의 색과 밑줄이 그어져 있는게 마음에 안든다.
4. posts를 한 폴더에 넣지 않고 카테고리별로 저장하고 싶다.
5. **Tistory처럼 Category가 sidebar에 바로 보여졌으면 좋겠다.**

현재 사용하고 있는 jekyll theme은 minimal mistakes인데,
sidebar는 기본 옵션이 아니었다. lanyon과 같은 다른 테마로 변경을 고민했다.

하지만 열띤 구글링의 결과,
현재 사용하고 있는 테마를 입맛대로 수정해서 쓰는 고수분들이 많았고,
그들의 도움을 받아 그냥 고치기로 하였다.

## 개선 내역

### favicon 추가

참고 글 : [How to apply favicon on minimal-mistake theme](https://ohjinjin.github.io/blog/favicon/)

favicon이란?

크롬 탭에 보이는 작은 아이콘을 의미한다.

브라우저에 따라 설정을 달리 해줘야 하는데, [realfavicongenerator.net](https://realfavicongenerator.net/)을 이용하면, 원하는 이미지만 선택하면 알아서 다 제공해준다. (Jekyll에서도 위 사이트를 권장하는 것 같다.)

### 폰트 변경

참고 글 : [GitHub Pages 기타 설정](https://devinlife.com/howto%20github%20pages/github-pages-settings/)

위 글이 참 작성되어 있다.
아래 두가지 개선 내역도 위 글을 참고하였다.

깃허브 커밋으로 링크가 다 달려있어서 코드를 바로 보고 이해할 수 있다.

> sass/minimal-mistakes/_reset.scss

```scss
  @include breakpoint($large) {
    /* devinlife : large 페이지 일때 폰트 사이즈 축소 20px->18px */
    /* font-size: 20px; */
    font-size: 19px;
  }

  @include breakpoint($x-large) {
    /* devinlife : x-large 페이지 일때 폰트 사이즈 축소 20px->18px */
    /* font-size: 20px; */
    font-size: 19px;
  }
```
해당 파일을 수정해서, 브라우저 크기에 따른 폰트 크기를 수정할 수 있다.

### 부제목으로 작성 일자 추가

기본 옵션으로 해당 글을 읽는데 소요되는 시간이 작성된다.
하지만 별로 필요 없다.
그래서 작성 일자로 수정해준다.

> _includes/archive-single.html

```html
<!--
    devinlife comments :
        아키이브 싱글 페이지(ex. 카테고리)에 각 포스트 제목 밑에 Updated 시간 표기
        기존에는 read_time이 표기. read_time -> date 변경
    -->
    <!-- if와 endif의 처음 \%는 %로 수정하고 복붙하기!-->
    {\% if post.date %}
      <p class="page__meta"><i class="far fa-fw fa-calendar-alt" aria-hidden="true"></i> {{ post.date | date: "%B %d %Y" }}</p>
    {\% endif %}
```

해당 파일을 수정해준다.

### 포스트 제목의 밑줄 없애기

> _sass/minimal-mistakes/_base.scss

```scss
/* links */

a {
  /* devinlife : a link 하이퍼링크 밑줄 없애기 */
  text-decoration: none;
  
  &:focus {
```
기본 옵션은 하이퍼링크에 다 밑줄을 달아준다.
안 이쁘다.
해당 파일에서 밑줄 옵션을 꺼준다.

## 남은 일들

- Custom sidebar : categories
  - Tistory처럼 카테고리를 바로 볼 수 있는 sidebar 추가하기.
- Landing page 만들기
  - 현재는 Index.html을 기본 그대로 사용하고 있는데, 좀 멋지게 만들고 싶다.