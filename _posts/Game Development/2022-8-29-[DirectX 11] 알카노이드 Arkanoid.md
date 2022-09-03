---
title: "[DirectX 11] 알카노이드 Arkanoid"
categories:
    - GameDevelopment
tags:
    - GameDevelopment
---

<iframe width="1280" height="720" src="https://www.youtube.com/embed/Qx3bwhJ2-tM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

<br>

dx11 충돌 실습을 위한 게임 '알카노이드' 제작

<br>

충돌 튕기기
- 공 - 벽, 벽돌, 바 간 충돌 시 공의 이동벡터를 변경
- AABB 충돌 함수에서 충돌 위치(좌우, 상하, 모서리)를 반환하도록 수정
- 좌우는 -y, 상하는 -x, 모서리는 -x, -y로 방향벡터 반전
- 바(bar)의 x값까지 공의 방향벡터에 더해줘 유저가 공의 방향을 의도적으로 조절할 수 있게 함
- 공은 벽돌 타입과 부딫힐 때마다 scalar 값이 점점 올라감

<br>

피격
- 벽돌은 공과 충돌 시 일정 시간 피격 이펙트(흰색 그라데이션 점멸) 효과
- 벽돌 종류마다 life가 다르며, life가 0이면 안 보이고 안 부딫히게 처리

<br>

아이템
- 2개 제작. 양 옆 아이템 벽돌을 부수면 효과 발생
    - 1 바에서 일직선 공이 나가 벽돌과 충돌 처리
    - 2 중앙에서 일정 범위 랜덤한 별들이 쏟아져 벽돌과 충돌 처리

<br>

재시작
- 모든 벽돌을 다 부수면 엔딩 화면 진입
- 키 입력으로 재시작, 초기화
