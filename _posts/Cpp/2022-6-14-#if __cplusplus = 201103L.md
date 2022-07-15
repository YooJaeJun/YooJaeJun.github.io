---
title: "#if __cplusplus >= 201103L"
categories:	
    - Cpp
tags:
    - Cpp
---

알고리즘 문제 풀이 때 자주 사용하는 헤더를 모아 사용하기 위해

Visual Studio 2022에 gcc의 pre-compiled header의 일종인 <bits/stdc++.h> 를 다운받은 후 include 했다.

한참 뒤 문제를 풀다가 unordered_map 혹은 unordered_set을 써야하는 상황에

막상 사용할 수 없지 않은가.

헤더를 확인해보니

![image](\assets\cplusplus\0.png)

내 cpp 버전이 97으로 되어있는 것 같았다.

구글링 후 아래 링크를 참고하여

<https://docs.microsoft.com/ko-kr/cpp/build/reference/zc-cplusplus?view=msvc-170>

![image](\assets\cplusplus\1.png)

속성 - 명령줄 - 추가 옵션에 /Zc:__cpluscplus 문구를 추가했다.

이후

![image](\assets\cplusplus\2.png)

__cplusplus 버전이 201402L로 C++ 14 기준으로 설정되며

unordered_map, unordered_set을 야무지게 사용할 수 있었다.

다른 컴퓨터에서 작업이나 알고리즘 문제 풀 일이 많으니

여기 기록해놓는다.

