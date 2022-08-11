---
title: "[DirectX 11] Screen 좌표계 to World 좌표계"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>

<iframe width="1280" height="720" src="https://www.youtube.com/embed/huVIos9X4Qc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<br>

- 마우스 좌표를 Screen 좌표계에서 월드 좌표계로 변환
    - mouseWorldPos.x = -app.GetHalfWidth() + mouseScreenPos.x + CAM->position.x;
    - mouseWorldPos.y = app.GetHalfHeight() - mouseScreenPos.y + CAM->position.y;
- 방향키로 카메라 이동 구현
- x, y 축 생성
- 화면 + 카메라pos 벗어나면 벗어나기 전으로 SetWorldPos() 시켜줌
