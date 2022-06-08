---
permalink: /Cpp/stringstream
title: "stringstream"
toc: true
toc_sticky: true
toc_label: "MYSELF"
categories:
    - Cpp
tags:
    - Cpp
---

C++에서 string을 특정 자료형의 문자들만 split해서 저장하고 싶을 때가 있다.

내가 자주 사용해야 했던 기능들을 정리하고,

항상 쓸 때마다 까먹거나 헷갈리는 stringstream 문법을 공부해보자.

우선 <sstream> 헤더를 포함하고

아래 예시와 같이 사용한다.

<br>
```cpp
#include <iostream>
#include <sstream>
using namespace std;

int main()
{
	int num;
	string str = "123 456 789";		// 공백 제외하고 숫자를 나누고자 함 -> int 타입의 변수들만 추출하자.
	stringstream stream;
	stream.str(str);	// 
	while (stream >> num) 	// 더 이상 num 의 자료형에 맞는 정보가 없을 때까지 계속 stream에서 num으로 자료를 복사.
	{
		cout << num << '\n';
	}
	stream.str("");		// 초기화. stringstream에 저장된 문자열을 삭제하고 싶을 때 사용.
}
```
```
123
456
789
```

<br>
num과 같은 int 타입의 문자들만 추출되었다.

stringstream은 "int에 맞는 자료가 없을 때까지" 추출해버린다.

또 다른 예시에서 확인해보자.


```cpp
#include <iostream>
#include <sstream>
using namespace std;

int main()
{
	int num;
	string str = "1 2 34 \n 5      6 7 \t 8 a 9 ";
	// 공백 / 제어문자(줄바꿈, 탭) / 다른 타입
	stringstream stream;
	stream.str(str);

	cout << "int split \n";
	while (stream >> num)
	{
		cout << num << ' ';
	}
}
```
```cpp
int split
1 2 34 5 6 7 8
```

테스트 결과,

1. 끝쪽 'a' 의 뒤에 있는 9는 생략된다. 즉, 'a' 전까지만 추출된다.
2. 줄바꿈, 탭 문자 등 제어문자는 생략하되 추출이 멈추지 않는다.

"int에 맞는 자료가 없을 때까지 추출해버린다"고 했다.

'a' 전까지 추출되는 것은 확인했다.

다만 공백, 제어문자(줄바꿈, 탭 등)는 char 혹은 string 타입으로 읽지 않는 것으로 보인다.

다만 개행문자와 같은

만일 뒤에 "a 50" 라는 문자열이 추가로 있어도

똑같이 "789" 까지만 추출한다.

더 나아가 실수 형태 + stream 두 번 추출했을 경우를 알아보자.

```cpp
#include <iostream>
#include <sstream>
using namespace std;

int main()
{
	int i;
	double d;
	string str = "1.4 2.545 2.0 .5 3.7f 4.5";
	// 일반적인 실수 / 소수점이 0 / '.5' 정수부 생략 / f로 float임을 명시
	stringstream stream;
	stream.str(str);

	cout << "int split \n";
	while (stream >> i)
	{
		cout << i << '\n';
	}
	stream.clear();	
	// stream.clear() : 첫 위치부터 다시 추출받기 위한 용도. 
	// string 끝까지 도달했는 flag가 올라가서 값이 추출되지 않기 때문 flag bit 초기화.
	cout << '\n';

	cout << "double split \n";
	while (stream >> d)
	{
		cout << d << '\n';
	}
}
```
```cpp
int split
1

double split
0.4
2.545
2
0.5
3.7

```

흥미로운 실험 결과다.

1. stringstream 2번: int로 1.0에서 1까지 추출되어, double 추출 시 0.4가 출력된다.
2. 일반적인 실수: cout 표준대로 출력된다.
3. 소수점이 0: cout 표준대로 출력된다.
4. '.5' 정수부를 생략: '0.5'로 생략된 숫자도 0으로 정해지고 출력된다.
5. f로 float임을 명시: float 형태를 표현하기 위해 'f'를 사용했지만 'f'는 char 타입이다. 그 전 3.7까지만 추출한다.
6. 마지막: 그 전 char 타입을 만나 추출되지 않는다.


<br>
이제 활용해보자.

알고리즘 문제에 유용하게 쓸 수 있는 경우가 많아서 확실히 기억해두려 한다.