---
title: "[DirectX 11] 슬라이딩 퍼즐 Sliding Puzzle"
categories:
    - GameDevelopment
tags:
    - GameDevelopment
---

<iframe width="1280" height="720" src="https://www.youtube.com/embed/2WhJKRUqqM4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

<br>

texture uv 좌표를 이용한 슬라이딩 퍼즐 제작

1. 여러 장의 이미지 생성 후, 위치는 고정, 규칙적으로 분할한 uv좌표를 랜덤 셔플해 대입
2. 퍼즐 이동: 방향키
3. 셔플: 각 이미지 uv 좌표 다시 랜덤 셔플
4. puzzleNum: 퍼즐 이미지 개수 재조정
5. cheat: 기록해둔 origin uv 대입

<br>

후기
- texture uv 좌표를 배우고 바로 활용할 수 있었다.
- 처음에는 분할한 uv좌표를 대입한 후, 위치를 랜덤으로 분포시켰는데,
- 퍼즐 이동 구현에 어려움이 있었다.
- 그냥 인덱스에 따른 위치는 고정한 후, 분할한 uv를 랜덤셔플해서 대입하는 게 구현이 용이했다.
