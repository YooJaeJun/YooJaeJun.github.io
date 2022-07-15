---
title: "[WinAPI] 탄막 슈팅 - C++ 문법과 디자인 패턴 -"
categories:
    - GameDevelopment
tags:
    - GameDevelopment
---

<iframe width="1280" height="720" src="https://www.youtube.com/embed/sMxKsHuLpsE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

☆ 탄막 슈팅 ☆
- 탄막을 피하며, 적에게 탄을 발사해 처치하는 2D 슈팅 게임



<br>

구현, 시뮬레이션
- 탄막 패턴, 스폰, 리스폰, 추격, 아이템, 이펙트, 무적 등
- matrix2x2 클래스 직접 만들어보기
- 이미지 회전 PlgBlt

![image](\assets\2022-7-7-WinAPI 탄막 슈팅 - C++ 문법과 디자인 패턴 -\1.png)
(가장 많이 고민했던 이미지 회전 기능)


수학
- vector, matrix

C++
- namespace
- get(), set()
- const 키워드
- 레퍼런스 전달에서 dangling pointer 의 위험
- noexcept 키워드
- default 키워드
- 소멸자 virtual
- 연산자 오버로딩
- assert
- 상속
- override, final 키워드
- enum hack
- enum class
- 클래스 간 연관관계가 필요할 때 전방선언 활용
- 스마트 포인터 std::shared_ptr<T> 
- 다운 캐스팅 dynamic_pointer_cast<T>(target)

디자인 패턴
- 싱글턴
