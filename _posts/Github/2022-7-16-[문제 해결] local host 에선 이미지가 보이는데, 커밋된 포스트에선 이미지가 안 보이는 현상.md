---
title: "[문제 해결] local host 에선 이미지가 보이는데, 커밋된 포스트에선 이미지가 안 보이는 현상"
categories:	
    - Github
tags:
    - Github
---

문제: local host 에선 이미지가 보이는데, 커밋된 포스트에선 이미지가 안 보이는 현상(깨지는 현상)

해결: .png => .PNG 혹은 .PNG => .png

이유: 로컬 호스트 영역에선 대소문자가 중요하지 않을 수 있으나, 웹을 통하면 확장자의 대소문자 구분도 중요해짐



[스택오버플로우 질문](https://stackoverflow.com/questions/42617768/images-show-up-locally-but-not-on-github-pages#comment72397900_42618313)
