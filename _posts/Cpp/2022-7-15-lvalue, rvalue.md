---
title: "lvalue, rvalue"
categories:	
    - Cpp
tags:
    - Cpp
---

## 요약

**lvalue**
- 단일 표현식 이후에도 없어지지 않고 지속되는 객체
- 주소가 있는 애들

**rvalue**
- 표현식이 종료된 이후에 더 이상 존재하지 않는 임시적인 값
- 리터럴, 임시변수, 임시객체



## 들어가기

lvalue: 왼쪽에 있는 값

rvalue: 오른쪽에 있는 값

기존엔 이런 단순한 개념이었다면 C++11 부터 개념이 다시 정의되고,

C++17부터 개념이 완성된다.



## 구조

모든 C++ 표현식에는 유형이 있고 value 카테고리에 속한다.

value 카테고리는 표현식 평가 중 임시 객체를 생성, 복사, 이동할 때 컴파일러가 따라야하는 규칙의 기초다.

C++17 표현식의 value 카테고리 정의

![image](\assets\2022-7-15-lvalue, rvalue\1\슬라이드1.PNG)


이러면 사실 무슨 말인지 감이 안 잡힌다.

개념을 정의하고 예시를 들어보자.



## 정의

**lvalue**
- 단일 표현식 이후에도 없어지지 않고 지속되는 객체
- 주소가 있는 애들
- 변수, const 변수, 배열 요소, lvalue 참조를 반환하는 함수, 비트필드, union과 class 멤버

**rvalue**
- 표현식이 종료된 이후에 더 이상 존재하지 않는 임시적인 값
- 리터럴, 비 참조 유형을 반환하는 함수 호출, 식 평가 중에 생성되지만 컴파일러에서만 액세스할 수 있는 임시객체
- 즉, 리터럴, 임시변수, 임시객체 



## 예시

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	int a = 3;		// 3: 리터럴 rvalue
	const int b = a;	// b: 수정 불가능한 lvalue
	int c = a + b;		// c: lvalue 	// a + b 연산 결과가 rvalue
	int* p;
	*p = a;			// *p: 참조되지 않은 포인터 lvalue

	const char* str = "hi";		// "hi": 임시변수
	cout << string("hello");	// string("hello"): 임시객체

	++a;	// lvalue. 증가된 자신을 리턴
	a++;	// rvalue. 증가된 복사본을 리턴

	&(++a);
	&(a++);	// error. 레퍼런스 연산자는 lvalue를 요구

	((a < 5) ? a : c) = 7;	// 조건 연산자 리턴: lvalue
}
```


## lvalue 참조자, rvalue 참조자

lvalue 참조자
- int& a = b;

rvalue 참조자
- int&& a = 10;


```cpp
#include <iostream>
#include <string>
using namespace std;

int rvalue() { return 10; }

int main()
{
	int lvalue = 10;
	
	int& a = lvalue;
	int& b = rvalue();	// error. int -> int &

	int&& c = lvalue();	// error. int -> int &&
	int&& d = rvalue();
}
```

rvalue 참조자는 Move Semantics의 구현을 가능하게 하고, 상당한 성능을 향상시킨다.

Move Semantics란 객체의 리소스(동적할당된 메모리 등)를 또 다른 객체로 이동하는 것.

이와 관련해서 별도 포스트에서 정리.



<br>

참고

<https://docs.microsoft.com/en-us/cpp/cpp/lvalues-and-rvalues-visual-cpp?view=msvc-170>

<https://effort4137.tistory.com/entry/Lvalue-Rvalue>

<https://hannom.tistory.com/208>



<br>

※ 틀리거나 개선할 부분이 있다면 알려주세요.