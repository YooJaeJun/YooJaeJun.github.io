---
title: "[Console] 섯다"
categories:
    - GameDevelopment
tags:
    - GameDevelopment
---

<iframe width="1280" height="720" src="https://www.youtube.com/embed/BUbL1UuhWfc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

<br>

섯다 게임 규칙 반영

1. 최초 각각 10,000원씩 지급
2. 한 판당 500원씩 차감
3. 우승 시 한 판 돈 몰아주기
4. 특수 기능 족보
5. 각 카드 조합에 따른 패 세트 구현
    - unordered_map으로 string을 키값으로, 순위를 value로 구현
    - unordered_map에서 find의 빠른 시간복잡도를 의도함

<br>

예외 처리
1. 동일 패일 시 선턴이 승리
2. 플레이어 수 입력
