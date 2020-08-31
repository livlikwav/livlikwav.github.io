---
title:  "GitKraken을 지운 김에 하는 Git 복습 #1"
excerpt: "터미널 하나로 다 해보려고 '재미삼아' 계속 도전 중!"
toc: true
toc_sticky: true

categories:
-  Tools
tags:
-  Git
last_modified_at: 2020-08-21TO22:30:00+09:00
---


### 그게 말이죠

처음에 Git bash로 시작하긴 했었다.
근데 너무 어려웠다.
윈도우 유저로만 살아왔고, 리눅스 수업은 열심히 안들었어서(지금은 후회중) 터미널은 나에게 너무 낯선 존재였다.

GitKraken이 Github 학생 등록하면 Pro 버전을 제공해주고,
확실히 GUI로 편하게 할 수 있어서,
GitKraken을 사용해왔다.

하지만, 요즘 Linux CLI도 배우고, Vim도 배운다고 터미널과 친해지기도 했고,
익숙해질때까지 Git도 CLI로 사용하라는 멘토님의 말씀에
Git CLI를 다시 공부하기로 했다.

Git 공식문서를 읽다가 어려워서, 블로그 글로 공부했던 기억이 나서 공식문서를 한번 쭉 읽으며 정리한다.

## 기록

[공식 문서는 늘 옳다.](https://git-scm.com/book/ko/v2)
(빨리 읽고 싶어서 한글로 훑고, 중요한 부분만 영문 참고)

### 1.1 버전 관리

VCS(Version Control System)

1. Local VCS
   1. RCS (Revision Control System)
   2. save patch set
2. CVCS (Central Version Control System)
3. DVCS (Distributed)
   1. Git!
   2. Clone all data of folder

### 1.2 Goal of Git

1. Speed
2. Simple design
3. Strong support for non-linear development
   1. thousands of parallel branches
4. Fully distributed
5. Able to handle large projects like the Linux kernal efficently
   1. speed and data size

### 1.3 What is Git

![delta_based](https://git-scm.com/book/en/v2/images/deltas.png)
델타 기반 버전관리 시스템은,
각 파일에 대한 변화를 저장한다.

![git_snapshot](https://git-scm.com/book/en/v2/images/snapshots.png)
이와 다르게, Git은 스냅샷을 저장한다.

- Snapshots, not differences
- a stream of snapshots

CVCS와의 차이, 개선점을 이해하는 것이 이해에 도움이 된다.
CVCS는 대부분의 명령어가 네트워크의 영향을 받는다.
> 계속 중앙 저장소에 코드를 올리고 커밋을 해야하므로

하지만 Git은 로컬 컴퓨터가 하나의 분산 저장소이다.
그래서 로컬에서 모든 명령어가 실행되고, 이것이 큰 장점이다.

![git_three_states](https://git-scm.com/book/en/v2/images/areas.png)
Git이 파일을 관리하는 상태는 3가지가 있다.

- Committed
  - 데이터가 로컬 데이터베이스에 안전하게 저장됐다.
- Modified
  - 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않았다.
- Staged
  - 현재 수정한 파일을 곧 커밋할 것이라고 표시했다.

3 main sections of a Git project

- Working Directory
  - a single checkout of the project
- Staging Area
  - a file, generally contained in your Git directory, that stores information about what will go into your next commit.
- .git directory(Repository)
  - where Git stores the metadata and object database for your project.
  - what is copied when you clone a repository from another computer

> 영어가 이해하기 더 표현이 명확한 것 같다.

### 1.4 Git CLI

**Git의 모든 기능을 지원하는 것은 CLI뿐**이다.
CLI를 사용할 줄 알면 당연히 GUI도 사용할 줄 안다.

### 1.6 Git Config

Configuration variables --> stored in the 3 different places

1. [path]/etc/gitconfig
   1. 시스템의 모든 사용자와 모든 저장소에 적용
2. ~/.gitconfig or ~/.config/git/config
   1. 시스템의 특정 사용자(현재 사용자)에 적용
3. config file in the Git directory (that is, .git/config)
   1. 특정 사용자에만 적용

Config는 Local한게 제일 우선해서 적용된다.

