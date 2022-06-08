---
permalink: /Cpp/cout 소수점 출력 fixed, precision
title: "cout 소수점 출력 fixed, precision"
toc: true
toc_sticky: true
toc_label: "MYSELF"
categories:
    - Cpp
tags:
    - Cpp
---

실수의 소수점 n자리를 출력하기 위해

printf() 는 다음과 같이 

'.소수점자릿수'를 형식문자 앞에 붙여 소수점을 쉽게 출력할 수 있었다.
<br>

```cpp
#include <iostream>
using namespace std;

int main()
{
    double d = 3.141592;
    printf("%.2lf", d);
}
```
```cpp
3.14
```

<br>
그렇다면 cout 출력방식은 소수점을 어떻게 표현할까?
<br>

```cpp
#include <iostream>
using namespace std;

int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);

    double d = 3.1415577;
    cout << d;
}
```
```cpp
3.14156
```
<br>

위 예시에서

일반적인 cout 출력 방식은 정수부+실수부 포함 6자리를,

끝자리는 소수점 반올림해서 표시된다.


<br>
특정 자릿수만 표현해보도록 하자.

우선, 실수부, 정수부를 포함해 n자리를 나타내는 방법이다.

```cpp
cout.precion(n);
```

위 예시에 cout 출력 전에 위 코드를 삽입하면

n == 실수부, 정수부를 포함한 자릿수

만큼 수가 출력된다.
<br>

```cpp
#include <iostream>
using namespace std;

int main()
{
	double d = 314.141592;
	cout.precision(12);
	cout << d;
}
```
```cpp
314.141592
```


원하는 소수점 자릿수까지 강제하여 표현하기 위해선
```cpp
cout << fixed;
```
<br>
코드를 cout.precision(n) 앞에 삽입하면 된다.
<br>

```cpp
#include <iostream>
using namespace std;

int main()
{
	double d = 314.141592;
	cout << fixed;
	cout.precision(12);
	cout << d;
}
```
```cpp
314.141592000000
```

거의 사용하진 않았지만,

```cpp
cout << fixed;
```

를 초기화 해주기 위해선

```cpp
cout.unsetf(ios::fixed);
```

코드를 추가해주면 된다.


```cpp
#include <iostream>
using namespace std;

int main()
{
	double d = 314.159;
	cout << fixed;
	cout.precision(5);
	cout << d << '\n';

	cout.unsetf(ios::fixed);
	cout << d << '\n';

	return 0;
}
```
```cpp
314.15900
314.16
```


사용처는 나 같은 경우 알고리즘 문제를 풀 때 

```cpp
ios::sync_with_stdio(0);
cin.tie(0);
cout.tie(0);
```
<br>
나는 위와 같이 C 표준 stream 과 C++ 표준 stream 의 동기화를 끊는 형태로 기본 폼을 구성하는데

이때 printf() 를 사용하지 않고 cout 만으로 소수점을 출력하고 싶을 때 사용한다.


<br><br>
문제 예시
<br/>
<https://www.acmicpc.net/problem/2754>

<br><br>
예시 코드
<br>

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int int64_t
using ll = long long;
using pii = pair<int, int>;
using vi = vector<int>;
using vvi = vector<vector<int>>;
#define yes cout << "YES\n";
#define no cout << "NO\n";
const int maxn = 1e9 + 7;
const double mod = 1e9 + 7;


map<string, float> dic;

void setDB()
{
	dic["A+"] = 4.3;	dic["A0"] = 4.0;	dic["A-"] = 3.7;
	dic["B+"] = 3.3;	dic["B0"] = 3.0;	dic["B-"] = 2.7;
	dic["C+"] = 2.3;	dic["C0"] = 2.0;	dic["C-"] = 1.7;
	dic["D+"] = 1.3;	dic["D0"] = 1.0;	dic["D-"] = 0.7;
	dic["F"] = 0.0;
}

void solution()
{
	setDB();
	string s;
	cin >> s;
	cout << fixed;
	cout.precision(1);
	cout << dic[s];
}

int32_t main()
{
	int t = 1;
	// cin >> t;
	for (int i = 0; i != t; i++) solution();
	return 0;
}
```

<br>
소수점 자릿수를 출력하고 싶다면 fixed, precision 을 알아두자.
