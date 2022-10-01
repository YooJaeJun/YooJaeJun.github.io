---
title: "[DirectX 11] Sound, Light, Alpha, Scene"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>
<iframe width="1280" height="720" src="https://www.youtube.com/embed/7FZoXGMe1Rc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

**프레임워크 Sound, Light, Alpha, SceneManager 클래스 학습**

Sound
- FMOD 라이브러리 이용
- 출력할 사운드 데이터에 대한 구조체 포인터를 map<string, SoundNode*> 형태의 컨테이너에 저장 (상수 시간의 탐색 위함)
- FMOD의 playSound 등 함수를 맵핑해 사용

<br>

Light
- 스크린좌표, 조명색 등의 정보가 담긴 구조체 버퍼
- 셰이더 언어 파일에 렌더링 파이프라인 PS 단계에서 라이트 작업 수행
- 조명 - 스크린 좌표계의 (0, 0) 간 사이의 거리와, 조명의 반지름을 측정하고, 
- 거리가 반지름보다 크면(조명 바깥 영역) 바깥색(outColor) rgb 값에 outColor rgb * 2.0f - 1.0f 를 더해줌
- 거리가 반지름보다 작거나 같으면(조명 안 영역) outColor rgb 값에 lightColor rgb * 2.0f - 1.0f 를 더해줌
- 그라데이션 라이트: (1.0f - 거리 / 반지름)인 값을, outColor rgb에 곱해줌.

<br>

Scene
- Sound와 같이 map<string, Scene*> 컨테이너 저장. 현재씬, 다음씬 정보 멤버 추가
- scene 불러오고 바뀌기전 지연시간: Update()문에서 지연시간 점감
- Scene01 등 클래스를 생성하고, Main문에서 최초 Change
- 이후 Scene 간 전환은 Scene 클래스에서 이루어짐
- Scene 간 데이터 공유가 필요하면 포인터 대입을 통해 필요한 객체 공유