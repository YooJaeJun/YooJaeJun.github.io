---
title: "[DirectX 11] Delaunay Triangulation 들로네 삼각분할"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>
<iframe width="1280" height="720" src="https://www.youtube.com/embed/r_HYmfGyxWQ?" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

1. 단계별 상태 패턴으로 분류
2. 일정 범위 랜덤한 크기의 사각형들, 일정 범위 랜덤한 범위 내 생성
3. 사각형들 간 충돌 시 벡터의 차로 밀어줌
4. 일정 크기 이상의 사각형들 선택
5. 들로네 삼각분할을 이용, 선택된 사각형 중점을 이어줌
- 깃허브의 외접원 공식과 들로네 삼각분할 코드를 참고
- 선과 삼각형 클래스가 없었기 때문에 프레임워크에 맞게 만듦
