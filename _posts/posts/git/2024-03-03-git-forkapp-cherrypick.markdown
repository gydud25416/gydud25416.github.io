---
layout: post
title:  "Git fork 앱으로 cherrypick commit 하기"
date:   2024-03-03 00:56:43 +0900
categories: 
    - posts
    - git
---

# Git fork 앱으로 cherrypick commit 하기 🍒

## 1. Chery-pick commit

### 1) git Cherry-pick이란?

1. this list will be replaced by the toc
{:toc .large-only}

- 제목과 마찬가지로 필요한 커밋만 골라서 가져오는 명령어다.
다른 브랜치에 있는 commit들 중에서 원하는 커밋만 내 브랜치로 가져와 수정사항을 커밋한다.
참고로 커밋을 브랜치끼리 옮기는 것이 아니라 동일한 커밋을 복사하는 개념이다.

### 2) cherry-pick은 언제 사용할까?

- 팀으로 협업할 때
    - **다른 동료가 만들고 있는 기능이 필요할 때.**
동료가 원하는 기능을 만들어 놨고, merge 까지 시간이 걸려 동료가 만든 **기능이 들어있는 commit만 골라서 가져올 수 있다.**
- 버그를 수정할 때
    - 새로운 기능을 개발하는 동안 버그가 발견될 때, **명시적으로 커밋을 만들어 해당 커밋만 골라서 master 브랜치에 배포**할 수 있다.
- 반영되지 않은 손실된 커밋 복원 (pull request)
    - 실수로 pull request를 merge 하기 전에 닫아버렸을 때, 체리픽을 사용해 **해당 commit을 가져와 살릴 수 있다.**

## 2. 사용 예시

master 브랜치에 **“애국가”** 브랜치를 추가하여 1절부터 4절까지 1절씩 commit했다.

master 브랜치에 **“애국가3절”** 브랜치를 추가하여 3절이 포함된 커밋을 추가하였다.

> 현재 fork 브랜치 상황
> 

![Full-width image](/assets/img/git/1-1.png)

<br />



🍒 **나의 목적은 “애국가” 브랜치에 빠진 3절을 “애국가 3절” 브랜치에서 가져와 master로 merge 시키는 것이다.** <br/>
{:.note}
  

<br />

![Full-width image](/assets/img/git/1-2.png)

“애국가” 브랜치를 checkout 한 후 “애국가 3절” 브랜치에 있는 애국가 3절을 추가한 커밋에서 cherry-pick Commit을 클릭했다.

![Full-width image](/assets/img/git/1-3.png)

두 브랜치의 파일이 같고 수정 위치가 겹쳐 conflict가 일어났다.

![Full-width image](/assets/img/git/1-4.png)

수정사항을 가져온 후 ‘현재 변경 사항 수락’을 클릭했다.

![Full-width image](/assets/img/git/1-5.png)

이대로 수정사항을 commit 하여 “애국가” 브랜치의 파일을 확인한다.

![Full-width image](/assets/img/git/1-6.png)

앞의 수정사항 모두 push한 후 master 브랜치를 checkout 하여 브랜치들을 merge시킨다.

![Full-width image](/assets/img/git/1-7.png)

![Full-width image](/assets/img/git/1-8.png)

master 브랜치의 남은 test.html
{:.figcaption}