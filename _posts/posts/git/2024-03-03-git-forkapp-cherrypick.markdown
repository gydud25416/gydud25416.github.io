---
layout: post
title:  "Git fork 앱으로 cherrypick commit 하기"
date:   2024-03-03 00:56:43 +0900
categories: 
    - posts
    - git
---

# 1. Chery-pick commit

### 1) git Cherry-pick이란?

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

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/87fe1d84-f227-40f2-8381-42dad26bb837/Untitled.png)

<aside>
🍒 나의 목적은 “애국가” 브랜치에 빠진 3절을 “애국가 3절” 브랜치에서 가져와 master로 merge 시키는 것이다.

</aside>

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/d2cc60d1-7721-4b03-8523-c13df179a515/Untitled.png)

“애국가” 브랜치를 checkout 한 후 “애국가 3절” 브랜치에 있는 애국가 3절을 추가한 커밋에서 cherry-pick Commit을 클릭했다.

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/7de7b8e7-3d90-4d7f-ac4f-e1e129870472/Untitled.png)

두 브랜치의 파일이 같고 수정 위치가 겹쳐 conflict가 일어났다.

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/3dfe8b17-5959-4d2a-87b9-984a9b93bb1a/Untitled.png)

수정사항을 가져온 후 ‘현재 변경 사항 수락’을 클릭했다.

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/4462b61f-4c3d-42da-85da-85657f1f9e9b/Untitled.png)

이대로 수정사항을 commit 하여 “애국가” 브랜치의 파일을 확인한다.

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/b97c2f4c-c8e2-4b63-a327-e52a5b2c3c06/Untitled.png)

앞의 수정사항 모두 push한 후 master 브랜치를 checkout 하여 브랜치들을 merge시킨다.

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/0752aa2f-e053-43f6-a294-e4e8b3dee7ae/Untitled.png)

![Full-width image](https://prod-files-secure.s3.us-west-2.amazonaws.com/58701d18-27cd-4023-b1ba-c7ee2604b3b6/7de4960a-6f65-4e40-99fc-61eb0b8116ef/Untitled.png)

master 브랜치의 남은 test.html
{:.figcaption}