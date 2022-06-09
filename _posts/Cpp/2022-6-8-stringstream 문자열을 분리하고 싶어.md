---
permalink: /Cpp/stringstream 문자열을 분리하고 싶어
title: "stringstream 문자열을 분리하고 싶어"
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

항상 쓸 때마다 까먹거나 헷갈리는 std::stringstream 문법을 공부해보자.

우선 <sstream> 헤더를 포함하고

아래 예시와 같이 사용한다.


```cpp
#include <iostream>
#include <sstream>
using namespace std;

int main()
{
	int num;
	string str = "123 456 789";	// 공백 제외하고 숫자를 나누고자 함 -> int 타입의 변수들만 추출하자.
	stringstream stream;
	stream.str(str);	// 현재 stream의 값을 str로 바꾼다.
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


<br>
---
<br>
일반적인 사용법은 여기까지만 알아두면 될 것 같다.
<br>

그치만 난 더 나아가 실수 형태 + stream 두 번 추출했을 경우를 알아보기로 했다.

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
	// string 끝까지 도달했다는 flag가 올라가서 값이 추출되지 않기 때문에, flag bit를 초기화.
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



<br><br>
이제 활용해보자.

```cpp
#include <iostream>
#include <sstream>
#include <string>
#include <vector> 
using namespace std;

// 시간 데이터를 받아 "~시 ~분 ~초" 형태로 표현하자.

int main(void) 
{
	string timeStr = "2022.06.08 15:01:20";		
	//연 월 일 시 분 초

	for (auto& timeCh : timeStr)
		if (timeCh == ':' || timeCh == '.')
			timeCh = ' ';
			// 추출이 멈추지 않기 위해 공백으로 바꿔준다.

	unsigned int num = 0;
	stringstream stream;
	stream.str(timeStr);
	vector<unsigned int> splitedTime;	// 출력 대신 저장해줄 공간

	while (stream >> num)
	{
		splitedTime.push_back(num);
	}

	vector<string> koreaTime{ "년", "월", "일", "시", "분", "초" };
	int idx = 0;
	for (auto& elem : splitedTime)
	{
		cout << elem << koreaTime[idx++] << ' ';
	}
	cout << '\n';

	return 0;
}
```
```cpp
2022년 6월 8일 15시 1분 20초
```

시간 데이터를 받아 "~시 ~분 ~초" 형태로 표현하자.

1. 추출을 멈추지 않기 위해 ':' 와 '.' 를 공백문자로 바꿔주었다.
2. stringstream으로 정수 타입 num으로 받고, splitedTime 배열에 넣어주었다.
3. 한국식 시간단위 표기를 배열로 저장하여, 분리된 시간 뒤에 붙여주었다.



<br>
---

마치며,

std::stringstream은 특히

알고리즘 문제에 유용하게 쓸 수 있는 경우가 많아서 확실히 기억해두자.




<br>
std::stringstream 내 함수
<br>
<https://www.cplusplus.com/reference/sstream/stringstream/>