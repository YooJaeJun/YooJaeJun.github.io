---
title: "[DirectX 11] 에어하키 Air Hockey"
categories:
    - GameDevelopment
tags:
    - GameDevelopment
---

<iframe width="1280" height="720" src="https://www.youtube.com/embed/uS0Wvsrw7Yc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

<br>

dx11 2D 충돌 처리, 벡터 실습을 위한 게임 '에어하키' 제작

2명이 공을 튕겨내 상대 골대에 넣는 게임

<br>

충돌
- 플레이어와 공 충돌 시 플레이어 scalar의 일정 비를 더하고 해당 방향으로 이동
- 공은 자신의 scalar가 높을수록 흰색에 가까워지게 그라데이션 효과
- 플레이어는 게임장 범위, 중앙선을 넘지 못하도록 처리

<br>

그  외 점수 및 시간 표시, 피격 처리 등
