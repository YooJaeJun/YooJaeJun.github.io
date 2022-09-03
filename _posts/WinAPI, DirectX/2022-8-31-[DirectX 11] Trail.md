---
title: "[DirectX 11] Trail"
categories:
    - WinAPIDirectX
tags:
    - WinAPIDirectX
---

<br>

<iframe width="1280" height="720" src="https://www.youtube.com/embed/oMs8QJw4X-s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<br>

Trail(잔상, 궤적) 효과 구현

<br>

deque 이용해 제작
- 배열, vector 등으로 풀링하듯이 사용해봤으나,
- 마지막에 있던 객체가 첫 객체로 돌아갈 때, layer 순서가 맞지 않는 문제가 있었음
- deque의 장점은 고정된 인덱스가 아니라는 점.
- deque를 사용하면 새 객체는 항상 가장 위에 렌더링 되기 때문에 deque를 채용해 trail 제작

<br>

타임
- trailTimer로 trail이 생성되는 시간 조절
- trailNum으로 trail의 최대 개수 조절
- trailDuration은 trailTimer * trailNum
- trailNum 갱신 시 다 지워주는 예외처리가 필요했음
