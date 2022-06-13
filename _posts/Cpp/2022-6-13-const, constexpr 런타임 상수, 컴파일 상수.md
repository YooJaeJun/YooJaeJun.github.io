---
title: "const, constexpr 런타임 상수, 컴파일 상수"
categories:
    - Cpp
tags:
    - Cpp
---

# const

- 상수를 선언하는 키워드

- const로 선언된 변수, 포인터, 멤버함수, 객체를 상수화 시킨다.

- 변수의 초기값을 변경할 수 없다.

- 선언시 const 변수는 컴파일과 동시에 *데이터 영역*  메모리로 올라간다.

- 선언과 동시에 초기화 해야한다.

```c
#include <stdio.h>

int main()
{
    const int size;  // 에러
}
```
```c
C 에러 없음
C++ 에러: 상수 변수 "maxSize"에 이니셜라이저가 필요합니다.
```

<br>

# C const

- C 언어에서 const 키워드로 선언된 변수는 런타임 상수

- 런타임 상수란? 컴파일 이후 프로그램이 실행될 때(런타임) 값의 대입이 이루어지는 상수

- C 언어에서는 const로 선언된 변수로 배열의 크기를 결정할 수 없다.

```c
#include <stdio.h>

int main()
{
	const int size = 4;
	int arr[size];   // 에러
}
```
```c
에러: 식에 상수값이 있어야 합니다.
```

<br>

# C++ const

- C++ 에서 const 는 맥락에 따라 컴파일타임 상수가 될 수도, 런타임 상수가 될 수도 있다.

- 초기화 될 값이 어떤 타임에 결정되는가에 따라, 컴파일타임 상수인지, 런타임 상수인지 결정된다.

```cpp
#include <iostream>

int main()
{
	const int size1 = 4;    // 컴파일타임 상수
	int arr[size1];	// 가능

	int num = 2;
	const int size2 = num;  // 런타임 상수
	int arr[size2];	// 에러. 런타임 상수이기 때문.
}
```
```cpp
에러: 식에 상수 값이 있어야 합니다.
변수 "size2" 값을 상수로 사용할 수 없습니다.
```

<br>

# C++ constexpr

- C++ 11부터 추가된 컴파일타임 상수 키워드

- 컴파일타임 상수임을 확실히 할 때 사용된다.

- constexpr은 항상 const지만, const는 항상 constexpr이 아니다.


```cpp
#include <iostream>
using namespace std;

int main()
{
	constexpr int myConstexpr(4);   // 컴파일타임 상수 초기화

	int num;
	cin >> num;
	constexpr int myConstexpr(num); // 에러. 런타임 상수 초기화
}
```
```cpp
에러: 식에 상수 값이 있어야 합니다.
변수 "num" 값을 상수로 사용할 수 없습니다.
```

<br>

# 결론

const, constexpr: 둘 다 상수로 만드는 키워드

const: 컴파일타임 상수, 런타임 상수 모두 만들 수 있음

constexpr: 컴파일타임 상수만 만들 수 있음

<br>

---

const와 constexpr의 기본적인 내용을 알아보고 비교해보았다.

constexpr은 cpp 클래스, 템플릿에서 자주 사용되며, 

C++ 14, C++ 20에서도 추가된 사항이 있는 것으로 보인다.

이후에 좀 더 상세한 내용을 공부해서 포스팅 해야겠다.
