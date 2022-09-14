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

여러 장의 이미지 생성 후, 위치는 고정, 규칙적으로 분할한 uv좌표를 랜덤 셔플해 대입
1. 이미지는 2차원형태로 나눔(나는 1차원 배열을 2차원 형태로 사용)
2. puzzleNum 수에 따라 수학식으로 이미지 월드 좌표 및 uv 좌표 판정 
(나는 스크린 좌표계, 월드 좌표계 변환식을 사용했으나, 다른 방법으로 pivot을 좌측상단으로 잡고, 이미지의 위치는 화면 좌표상단을 기준으로 로컬 좌표를 활용하는 방법이 더 낫겠다 싶음)
3. 보이지 않는 위치의 이미지만 렌더링 하지 않음
4. 퍼즐 이동: 방향키 입력 시 렌더링하지 않았던 이미지의 uv 좌표에, 이동할 위치에 있는 uv 좌표를 대입
5. 셔플: 각 이미지 uv 좌표 다시 랜덤 셔플
6. puzzleNum: 퍼즐 이미지 개수 재조정
7. cheat: 기록해둔 origin uv 대입

<br>

후기
- texture uv 좌표를 배우고 바로 활용할 수 있었다.
- 처음에는 분할한 uv좌표를 대입한 후, 위치를 랜덤으로 분포시켰는데,
- 퍼즐 이동 구현에 어려움이 있었다.
- 그냥 인덱스에 따른 위치는 고정한 후, 분할한 uv를 랜덤셔플해서 대입하는 게 구현이 용이했다.
