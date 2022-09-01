---
title: "[STL] deque 활용 문제"
categories:	
    - PS
tags:
    - PS
---

## 요약

double-ended queue

C++ STL Sequence Container

배열 or Linked List를 기반으로 추상화한 데이터 구조

다른 곳에 사용법은 많으니 사용법은 간단히 요약하고, 공부하며 직접 활용한 문제를 복기하고자 한다.

<br>

## 원형

(C++17 이전 기준)

```cpp
template<
    class T,
    class Allocator = std::allocator<T>
> class deque;
```

Type을 받는 템플릿 클래스

사용 방법은 vector와 같다.

<br>

## 사용법

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main()
{
	deque<int> dq;		// deque 객체 선언
	deque<int> temp(10, 1);		// 원소 10개 생성 후 각각 1로 초기화
	dq = temp;		// 대입

	if (dq[0] == dq.at(0))	// dq index 표현들
	{
		cout << "2번 인덱스: " << dq.front() << "\n\n";
	}

	dq.push_back(2);	// 삽입
	dq.push_front(3);
	cout << "뒤2, 앞3 추가\n";

	for (auto iter = dq.begin(); iter != dq.end(); iter++)	// iterator 순회
	{
		cout << *iter << ' ';
	}
	cout << "\n\n";

	dq.erase(dq.begin());	// 위치 지정 삭제
	cout << "index 0 erase\n";
	
	dq.pop_back();	// 맨 뒤 삭제
	cout << "pop_back\n";

	dq.resize(15);	// 리사이즈. 추가된 값은 0으로 초기화됨
	cout << "15로 resize\n";

	for (auto& elem : dq) cout << elem << ' ';
	cout << "\n\n";


	cout << "find 1" << '\n';
	if (find(dq.begin(), dq.end(), 1) != dq.end())	// find. 찾으면 찾은 위치 인덱스, 못 찾으면 dic.end() iterator 반환
	{
		cout << "value 1 찾았따." << '\n';
	}
	else
	{
		cout << "value 1 못!!! 찾았당." << '\n';
	}
	cout << '\n';


	dq.clear();		// 모두 제거
	cout << "dq 다 지웠당\n";

	cout << "dq size: " << dq.size() << '\n';		// 사이즈
	cout << "dq.empty() ? " << dq.empty() << '\n';	// 비어있는지

	return 0;
}
```
```cpp
2번 인덱스: 1

뒤2, 앞3 추가
3 1 1 1 1 1 1 1 1 1 1 2

index 0 erase
pop_back
15로 resize
1 1 1 1 1 1 1 1 1 1 0 0 0 0 0

find 1
value 1 찾았따.

dq 다 지웠당
dq size: 0
dq.empty() ? 1
```

다른 STL과 같이 공통 시퀀스들을 사용한다.

vector와 달리 **push_front(), pop_front()** 메서드를 지원하며

push_front(), pop_front(), push_back(), pop_back() 시간 복잡도가 무려 **O(1) 상수 시간**을 보장한다.

vector처럼 **임의 접근**(random access)이 **O(1)**로 가능하다.

역시 **찾기**(find)는 **O(n)**.

**중간 구간 삽입 및 삭제**는 n / 2 가 걸리므로, Big-O 표기법에 의해 **O(n)**이다.

<br>

## 사용처

deque는 앞뒤 삽입, 삭제가 잦은 구조에 많이 사용한다.

게임 개발 공부할 때는 궤적, 잔상 구현에 썼다.

근데 deque는 문제 풀 때는 다른 컨테이너에 비해 많이 사용하진 않은 것 같다.

그래도 STL 중에서 많이 안 썼다는 뜻이지 문제는 꽤 많다. 다시 복기해보자.


<br>

## 문제

[백준 10866 Siver 4 덱](https://www.acmicpc.net/problem/10866)

덱의 주요 메서드를 모두 사용할 수 있는 문제

교육용 문제 추천

[백준 10866 Siver 4 덱, 내풀이](https://github.com/YooJaeJun/PS-Baekjoon-Programmers/blob/main/%EB%B0%B1%EC%A4%80/Silver/10866.%E2%80%85%EB%8D%B1/%EB%8D%B1.cc)

<br>

[백준 2346 Siver 4 풍선 터뜨리기](https://www.acmicpc.net/problem/2346)

해당 index를에 쓰인 수 만큼 이동한 후 전 index를 제거하는 것을 반복하는 문제

생각만큼 쉽지 않은 이유는 deque는 삽입 삭제 시 인덱스가 계속 바뀌는데, 답은 원래의 인덱스를 계속 기억해야 하기 때문이다.

하지만 맨 앞과 맨 뒤 간 이동을 한 칸이라 치기 때문에, 원형 구조란 것을 알 수 있고,

'이동' 개념이 deque의 앞의 걸 뒤에 옮기거나 뒤의 걸 앞에 옮기는 방식으로 생각해 deque를 사용했다.

인덱스에 쓰인 수가 양수냐 음수냐에 따라 앞의 걸 뒤에 옮길지, 뒤의 걸 앞에 옮길지만 생각하면 된다.

이걸 반복하면 완료

[백준 2346 Silver 4 풍선, 내풀이](https://github.com/YooJaeJun/PS-Baekjoon-Programmers/blob/main/%EB%B0%B1%EC%A4%80/Silver/2346.%E2%80%85%ED%92%8D%EC%84%A0%E2%80%85%ED%84%B0%EB%9C%A8%EB%A6%AC%EA%B8%B0/%ED%92%8D%EC%84%A0%E2%80%85%ED%84%B0%EB%9C%A8%EB%A6%AC%EA%B8%B0.cc)

<br>

[프로그래머스 Level 2 프린터](https://school.programmers.co.kr/learn/courses/30/lessons/42587)

맨 앞서부터 우선순위 젤 높으면 뽑고, 다른 더 높은 게 있으면 맨 뒤로 보내고를 반복해서 다 뽑는 문제다.

단 location, 즉 원래 index가 몇 번째로 뽑혔는지 알아야 하기 때문에 

deque<pair<int, int>> 로 수와 index를 세트로 저장해두어야 했다. (혹은 구조체를 만들던지)

하나라도 큰 게 나오면 맨 앞에 걸 맨 뒤에 보내주고, 아니면 flag를 활용해 뽑으면 됐다.

[프로그래머스 Level 2 프린터, 내 풀이](https://github.com/YooJaeJun/PS-Baekjoon-Programmers/blob/main/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4/lv2/42587.%E2%80%85%ED%94%84%EB%A6%B0%ED%84%B0/%ED%94%84%EB%A6%B0%ED%84%B0.cpp)

유사한 문제로 **백준 1966 Silver 33 프린터 큐** 문제가 있다.

<br>

[백준 3190 Gold 4 뱀](https://www.acmicpc.net/problem/3190)

스네이크 게임 구현 문제

구현하라는대로 구현하면 된다.

뱀의 몸체를 deque으로 구현해 꼬리를 한 칸 없애고 머리에 한 칸 추가하는 식으로 구현했다.

그외에 충돌 처리를 위해 맵에도 이 칸이 비었는지, 뱀이 있는지도 판단해야 한다.

덱을 어떻게 활용할지 실전에 가까운 문제라 재밌게 풀었다.

디버깅이 쉽지 않아 한 번 실수하면 찾는 데 시간이 좀 걸릴 것 같다.

[백준 3190 Gold 4 뱀, 내 풀이](https://github.com/YooJaeJun/PS-Baekjoon-Programmers/blob/main/%EB%B0%B1%EC%A4%80/Gold/3190.%E2%80%85%EB%B1%80/%EB%B1%80.cc)


<br>

참고

[cppreference - deque](https://github.com/YooJaeJun/PS-Baekjoon-Programmers/blob/main/%EB%B0%B1%EC%A4%80/Gold/3190.%E2%80%85%EB%B1%80/%EB%B1%80.cc)


<br>

※ 틀리거나 개선할 부분이 있다면 알려주세요.