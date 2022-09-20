---
title: "[DirectX 11] 숫자 폰트 이미지 Number Font Image"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>

<iframe width="1280" height="720" src="https://www.youtube.com/embed/cPh3Bu9_3mU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

1. 이차원 배열 형태의 폰트 이미지 배열. 자릿수 - 1~10숫자이미지
2. 각 자릿수에 맞게 위치를 초기화할 때 세팅
3. anchor 구현: 해상도 상 우측하단에 위치하도록 함
4. 스코어를 받아옴
5. 스코어 맥스 자릿수 - 1이면 0을 더해줌. '9'라면 '09'로 표기하기 위함
6. 마지막 자릿수부터 숫자 이미지 키고 꺼줌
