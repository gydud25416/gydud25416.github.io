---
layout: post
title:  "Git fork 앱으로 rebase 하기"
date:   2024-03-11 00:57:43 +0900
categories: 
    - posts
    - git
---

# Git fork 앱으로 rebase 하기 🧨

## rebase란?

* this list will be replaced by the toc
{:toc .large-only}

- base를 다시 맞춘다.
- 작업을 하기 위해 ROOT 브랜치에 브랜치 하나를 만든 상황에서 ROOT 브랜치에 추가로 커밋이 생겼을 때



**특정 브랜치 A**에서 **다른 브랜치 B**를 파서 작업을 하고 있었는데 **A 브랜치**에 다른 사람이 추가로 커밋을 올렸다.

브랜치 B에서 브랜치 A 로 merge를 시키려고 할 때 A에 있는 커밋이 없는 상태라 conflict가 생기게 된다.

![Untitled](/assets/img/git/rebase/1.png)

rebase를 하게 되면 **특정 브랜치 A**의 Head에 맞춰 그 뒤로 **브랜치 B**에서 쌓은 커밋들이 쌓이게 된다. 

![Untitled](/assets/img/git/rebase/2.png)

브랜치 B의 커밋이 달라지게 된다.

이때 로컬과 리모트의 상태가 달라지게 될 수 있어 강제 푸쉬가 필요할 수 있다.

1) 사용 예시


> 💫 ROOT 브랜치에서 가사 2줄을 커밋한 후 제목을 추가하는 브랜치를 만들었다.
그 후 root 브랜치에서 가사 3줄, 가사 4줄을 커밋했고,
애국가 제목을 추가한 브랜치를 root 브랜치로 merge하고자 하다.
{:.lead}

![Untitled](/assets/img/git/rebase/3.png)

“애국가 제목추가” 브랜치를 “애국가 가사”브랜치에 merge시켰는데 merge가 되었다.

그래서 main 브런치에 모두 merge한 후 main 브랜치에서 애국가 2절 브랜치를 만들었다.


> 💫 현재 main은 애국가 1절이고(root 브랜치) 2절 브랜치를 만든 후 merge를 시도했다.
{:.lead}

![Untitled](/assets/img/git/rebase/4.png)

main으로 merge 시도하니 conflict가 일어나 abort 시켰다.

**“애국가 2절가사”** 브랜치를 check out하여 “Rebase ‘main’ to Here…” 을 클릭했다.

> 💫 “애국가 2절가사”에 없는 1절 브랜치의 커밋들이 전부 conflict 된다.
해당 사항을 전부 수정 후 커밋한다.
{:.lead}

![Untitled](/assets/img/git/rebase/5.png)

![Untitled](/assets/img/git/rebase/6.png)

![Untitled](/assets/img/git/rebase/7.png)

main 브랜치에 있던 커밋들이 전부 conflict되어 전부 수정한다.

![Untitled](/assets/img/git/rebase/8.png)


>💫 전부 수정하면 **애국가 2절 브랜치**에 root 브랜치(main) 커밋들이 추가된 채로 root 브랜치(main)로 합쳐진다.
{:.lead}

![Untitled](/assets/img/git/rebase/9.png)

이대로 main 브랜치를 푸시하면 pull을 받아야하는 상황이 생겨 강제로 force push를 해야한다.

![Untitled](/assets/img/git/rebase/10.png)

push가 끝나면 **애국가 2절가사**를 base로하여 **main의 커밋들이 위로 쌓인것을 볼 수 있다.**

![Untitled](/assets/img/git/rebase/11.png)

github로 돌아가 결과물을 확인한다.

![Untitled](/assets/img/git/rebase/12.png)
