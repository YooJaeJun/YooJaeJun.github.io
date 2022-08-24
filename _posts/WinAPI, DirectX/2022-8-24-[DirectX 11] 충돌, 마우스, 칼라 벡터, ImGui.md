---
title: "[DirectX 11] 충돌, 마우스, 칼라 벡터, ImGui"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>

<iframe width="1280" height="720" src="https://www.youtube.com/embed/--Sw0SkZ2rk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<br>

충돌
- 사각형과 점 충돌
    - 점이 사각형 각 꼭지점 내부에 위치한지 검사
    - main -> GameObject -> Utility. 즉, 실제로 Utility에서 조건 체크.

<br>

마우스
- INPUT 싱글톤 객체로로 마우스 좌표 받기

<br>

칼라 벡터
- RGB 중 B 값은 고정.
- 방향: 마우스 좌표 - 사각형 좌표 벡터의 차로 구함
- 방향 normalize()
- Color(dir.x, dir.y, 0.5f, 1.0f); 로 정규화된 방향(0.0~1.0)에 따라 R, G 값 바꾸기

<br>

ImGui
- Directx 11 UI 라이브러리 사용
- SliderFloat, InputFloat3, InputInt3 사용해서 테스트