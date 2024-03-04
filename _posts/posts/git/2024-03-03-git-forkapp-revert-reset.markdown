---
layout: post
title:  "Git fork 앱으로 revert, reset 하기"
date:   2024-03-03 00:57:43 +0900
categories: 
    - posts
    - git
---

# Git fork 앱으로 revert, reset 하기 ⏱

> 이전 돌아가고 싶은 커밋으로 가고 싶을 때 사용하거나, master 브랜치로 릴리즈를 했는데 치명적인 버그로 인하여 롤백해야 한느 경우 이전 커밋으로 되돌아가기 위해 사용한다.
> 

## reset, revert의 차이

- 둘다 이전 커밋으로 되돌린다는 점에서는 동일하지만
다른 사람간의 코드 공유의 유(revert) 무(reset)에 따라 달라진다.

## 1. reset을 사용하는 경우

- commit을 삭제하고 싶을 때
- 혼자만 사용하는 브랜치인 경우
- origin에 있지만 아무도 이 브랜치를 사용하지 않는다는 확신을 가지는 경우
- 단, 이미 push를 한 내용을 변경하려면 force push를 사용해야 한다.

### 1) reset 옵션

```
**--soft** :커밋에 사용된 것들을 전부 보존하며, staged 상태로 되돌린다. (add 상태)

**--mixed :**생략 시 기본 옵션이며,커밋에 사용된 것들을 전부 보존하고, unstaged 상태로 되돌린다. (add 이전 상태)

**--hard :**커밋에 사용된 것들을 전부 "삭제"한다.즉, 없었던 일로 만든다고 생각하면 된다. (되도록 사용하지 않는 걸 권장한다.)
```

 

### 2) 사용 예시

master 브랜치에 “애국가” 브랜치를 만들어 1절부터 4절까지 각각 commit하며 추가했다.

![Untitled](/assets/img/git/2-1.png)


> 💫 해당 3절과 4절에서 오타를 발견하여 2절로 되돌아가려고 한다.
{:.lead}

#### - 공통점

- soft, mixed, hard 모두 브랜치에서 커밋이 사라진 것을 볼 수 있다.

![Untitled](/assets/img/git/2-2.png)



> **soft reset**
> 💫 수정 사항이 stage에 있고 커밋이 보존된 상태
{:.lead}

![Untitled](/assets/img/git/2-3.png)

> **mixed reset**
> 💫 기본 옵션으로 수정 사항이 unstage에 있고 커밋이 보존된 상태
{:.lead}

![Untitled](/assets/img/git/2-4.png)

> **hard reset**
> 💫 수정사항, 커밋 전부 삭제한다. 즉, 없었던 일로 만든다.
{:.lead}

![Untitled](/assets/img/git/2-5.png)

## 1. revert 사용하는 경우

- 원격 저장소의 저장된 상태의 커밋을 취소하고 싶을 때
- 커밋 이력 자체를 지우기보단, 해당 커밋에서 사용한 것들을 **취소한 새로운 커밋을 만든다.**

### 1) 사용 예시

![Untitled](/assets/img/git/2-6.png)

애국가 브랜치에서 3절과 4절의 오타를 발견하여 2절로 되돌리려고 한다.

![Untitled](/assets/img/git/2-7.png)

2절 커밋으로 revert를 누르니 3절, 4절의 변경사항과 섞여 conflict가 일어났다.

**변경사항을 모두 삭제(수신 변경 사항)**하거나 **오타를 수정(현재 변경 사항)**하여 commit한다.

- 오타 수정하여 commit (현재 변경 사항 수락)

![Untitled](/assets/img/git/2-8.png)

![Untitled](/assets/img/git/2-9.png)

![Untitled](/assets/img/git/2-10.png)


> 💫 reset은 커밋과 오류사항을 삭제 할 수 있다면, revert는 삭제에 더해서 수정까지 하여 commit을 남길 수 있다.
{:.lead}