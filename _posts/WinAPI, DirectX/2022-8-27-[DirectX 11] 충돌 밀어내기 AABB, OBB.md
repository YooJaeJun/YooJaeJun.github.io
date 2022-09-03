---
title: "[DirectX 11] 충돌 밀어내기 AABB, OBB"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>

<iframe width="1280" height="720" src="https://www.youtube.com/embed/BeRRtyPMIj0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<br>

충돌 AABB

사각형과 점
- 점이 사각형의 좌우상하 내부 판단

원과 원
- 두 중심점 사이의 거리와 반지름 합 간 비교

원과 사각형
- 사각형의 좌우, 상하, 모서리 부분 충돌 따로 판단
- 사각형 길이에 원의 반지름만큼 더 긴 가상의 사각형을 두고, 
- 사각형 안에 원의 중점이 있으면 충돌 판단. 상하, 좌우 충돌 판단
- 모서리는 원과 사각형 모서리 점 간의 충돌 판단

<br>

충돌 OBB

사각형과 사각형
- 회전된 도형의 충돌 체크
- 각 사각형 x, y축 벡터에 투영
- 내적으로 평행한 직선에 투영된 크기를 얻어
- 각 사각형 축 벡터가 투영된 길이의 합과 
- 두 사각형 중심 간 거리를 비교해 두 중심 간 거리가 더 짧으면 충돌
- 4개의 축 반복

<br>

밀어내기
- 저번 마우스 좌표 받아오기, 마우스 좌표와 충돌을 이용,
- 마우스로 끌고 온 도형과 충돌 시 충돌된 도형에 
- **마우스 좌표의 이동벡터**를 반영해 마우스가 이동하는 속도로 이동
- '밀어내는' 효과를 주는 의도