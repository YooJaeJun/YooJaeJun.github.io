---
title: "istringstream, ostringstream"
categories:
    - Cpp
tags:
    - Cpp
---
지난 std::stringstream 에 이어...

비슷한 문자열 파싱 함수 2가지를 더 공부해야겠다.

stringstream 관한 내용은 전 글 참고...
<br>

---
<br>
stringstream은 삽입, 추출 연산자를 모두 사용할 수 있기 때문에

후에 연산자를 잘못 써 실수할 여지도 있고, 

코드를 볼 때 입력을 받을 기능인지 출력할 기능인지 더 명시해줄 필요가 있을 것이다.


"<<" : 삽입 연산자

">>" : 추출 연산자

"istringstream": 삽입 연산자가 정의되어 있지 않음.
"ostringstream": 추출 연산자가 정의되어 있지 않음.

<br>

# 1. istringstream

string을 입력받아 다른 타입으로 바꿔주는 기능

전에 포스트했던 stringstream 사용법과 같다.

```cpp
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
	string str = "yoo study 777";
	istringstream iss(str);

	while (iss >> str)
	{
		cout << str << '\n';
	}

	return 0;
}
```
```cpp
yoo
study
777
```

<br>

# 2. ostringstream

분리된 string을 조립하거나, 특정 수치를 문자열로 변환하기 위해 사용

```cpp
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
	const int n = 5;
	string str[n] = { "yoo", "study", "777", "  ", "0.55" };
	ostringstream oss;
	for (int i = 0; i < n; i++)
	{
		oss << str[i];
	}
	cout << oss.str() << '\n';

	return 0;
}
```
```cpp
yoostudy777  0.55
```

<br>

# 3. 활용 - getline()

추가로, stringstream과 std::getline() 을 활용한 예제다.

getline()은 개행문자나 특정 문자를 읽게 되면 읽어들이기를 종료하는 함수다.

```cpp
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main() {
	string str = "yoo@study@777";
	istringstream iss(str);
	string buffer;
	while (getline(iss, buffer, '@'))
	{
		cout << buffer << '\n';
	}

	return 0;
}
```
```
yoo
study
777
```


전 포스트부터 지금까지 stringstream, istringstream, ostringstream 에 대해 공부했다.

문자열 파싱 관련 알고리즘 문제가 나오면 사용해봐야겠다.
