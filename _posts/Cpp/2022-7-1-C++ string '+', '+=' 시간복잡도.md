---
title: "C++ string '+', '+=' 시간복잡도"
categories:	
    - Cpp
tags:
    - Cpp
---

## 미리 보는 결론

C++ std::string의 operator+, operator+= 연산자 오버로딩의 시간복잡도는 다르다.

- str += 'a';	// 시간복잡도 O(1)
- str = str + 'a'	// 시간복잡도 O(n)
- str = 'a' + str	// 시간복잡도 O(n)


==> 되도록 operator+=() 를 사용하자.

<br>

알고리즘 문제를 풀며 string 삽입 연산이

시간 복잡도가 왜 이렇게 나오는지 궁금해져서 포스트함

<br>

## 1. str += 'a';

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string str;
	const int n = 1'000;
	for (int i = 0; i < n; i++)
	{
		str += 'a';
	}
	return 0;
}
```

시간 복잡도 : O(n)

str 마지막에 'a'가 추가됨. O(1)을 n번 반복 == O(n)


<br>

## 2. str = str + 'a';

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string str;
	const int n = 1'000;
	for (int i = 0; i < n; i++)
	{
		str = str + 'a';
	}
	return 0;
}
```

시간 복잡도 : O(n^2)

매번 새로운 문자열 대입 O(n)을 n 번 반복 == O(n^2)


<br>

## 3. str = 'a' + str;

시간 복잡도 : 2번 케이스와 동일

str 맨 앞에 'a' 붙인 문자열 생성 후 대입


<br>

## 결론

C++ 에서 string에 문자를 push_back 하는 연산은 operator+=() 연산자를 사용하자.


## 참고

<https://en.cppreference.com/w/cpp/string/basic_string/operator%2B>