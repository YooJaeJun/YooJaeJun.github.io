---
title: "C++ Values (lvalue, rvalue, xvalue) 요약"
categories:	
    - Cpp
tags:
    - Cpp
---

## 요약

C++ 11 이전 

	lvalue
		주소가 있는 값
		표현식이 끝난 후에도 사라지지 않는 값

	rvalue
		주소가 없는 값
		표현식이 끝난 후에 사라지는 값

C++ 11 이후 

	lvalue
		식별성(Identity)이 있고
		move 될 수 없는 값

	prvalue
		식별성이 없고
		move 될 수 있는 값

	xvalue
		식별성이 있고
		move 될 수 있는 값
			ex. rvalue 캐스팅 static_cast<T&&> ..
			std::move(x)


## 후기

[lvalue rvalue 정리](https://yoojaejun.github.io/cpp/lvalue,-rvalue/)

위 링크에서 예전에 lvalue와 rvalue를 정리했었다.

이번엔 xvalue에 주목하여, 다른 자료를 참고하지 않고 간단하게 정리해보았다.


<br>

※ 틀리거나 개선할 부분이 있다면 알려주세요.