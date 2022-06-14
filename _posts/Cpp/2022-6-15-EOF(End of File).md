---
title: "EOF(End of File)"
categories:	
    - Cpp
tags:
    - Cpp
---

EOF(End of File): 파일의 끝

더 이상 읽을 데이터가 없다는 의미다.

백준을 풀다보면 test case num 이 주어지지 않았는데

입력을 여럿 받아야 하는 경우가 있었다.

이때 EOF를 이용하여 파일이 종료될 때까지 입력을 받는 코드를 작성해야 했다.

<br>

# C++ style

```cpp
#include <iostream>
using namespace std;

int main()
{
	int n1, n2;
	while (cin >> n1 >> n2)
	{
		cout << n1 + n2 << '\n';
	}

	return 0;
}
```

입력

```cpp
1 2
3 4
^Z
```

출력

```cpp
3
7

```

while (cin >> n1 >> n2) 는 **에러가 있거나 파일의 끝을 만났을 때** false를 반환한다.

콘솔에서 종료를 위해 Windows는 **Ctrl + z** (^Z == Ctrl + z)를, 

Unix, Linux, Mac OS X는 Ctrl + d 를 한 번 입력해야 한다. 

이처럼 입력이 없을 때까지 계속 입력을 받을 수 있다.

이때 정상 종료된다면 입력이 없을 때까지 계속 입력을 받을 수 있으며, 

믿고 백준 문제를 제출해도 될 것이다.

<br>
다만 다음과 같은 사용은 조심해야했다.

```cpp
#include <iostream>
using namespace std;

int main()
{
	int n1, n2;
	while (cin.eof() == false)
	{
		cin >> n1 >> n2;
		cout << n1 + n2 << '\n';
	}
	
	return 0;
}
```

cin.eof()는 EOF를 만나면 값이 true가 된다.

그럼 cin.eof()는 EOF를 만나지 않은 것일까?

블록 안의 cin은 엔터('\n')를 버리지 않고 버퍼에 남긴다.

마지막 수를 입력 받은 뒤 개행 문자가 남아있어 아직 EOF가 아니다.

결국 cin.eof()는 false를 반환한다.

그리고 블록으로 들어가 무한정 입력 대기 상태에 빠진다.

cin.eof()를 사용하려면 cin이 버퍼에 남긴 엔터를 처리해줘야한다.

<br>

# getline(cin, str)

만일 문자열을 받는다면, string 헤더를 추가하고,

getline()을 사용할 수도 있다.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
	string str;
	while (getline(cin, str)) {
		cout << str << '\n';
	}

	return 0;
}
```
```cpp
asdf
asdf
qwer
qwer
^Z

```

getline()은 엔터('\n')를 무시하지 않고

하나의 입력으로 받아 엔터를 버린다(버퍼에 남기지 않는다).

굳이 cin.eof()를 사용하고 싶다면, getline()과 같이 써야한다.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
	string str;
	while (cin.eof() == false) {
		getline(cin, str);
		cout << str << '\n';
	}

	return 0;
}
```
```cpp
asdf
asdf
qwer
qwer
^Z

```

<br>
그렇다면 C style로 scanf로도 할 수 있지 않을까?

<br>

# C style

```c
#include <stdio.h>

int main()
{
	int n1, n2;
	while (scanf_s("%d %d", &n1, &n2) != EOF)	// EOF는 값이 -1인 매크로
	// while (~scanf_s("%d %d", &n1, &n2))		// 비트 NOT 연산자를 사용할 수도 있다.
	// while (scanf_s("%d %d", &n1, &n2) == 2)	// 값을 입력받는 개수와 비교할 수도 있다.
	{
		printf("%d \n", n1 + n2);
	}

	return 0;
}
```
```c
1 2
3
3 4
7
^Z
^Z
^Z

```



C 스타일의 scanf_s는 성공적으로 입력받은 문자를 return하는데

**에러가 있거나 파일의 끝을 만났을 때** -1을 리턴한다.

다만 cin.eof() 와는 다르게 **scanf_s는 Ctrl + z와 Enter를 세 번 입력**해야 콘솔창이 종료된다!

왜 scanf_s는 3번 입력해야하는지??

게시글을 여럿 뒤져보았으나, 이와 관련해선 결국은 명확한 이유를 찾지 못했다.

<br>

# EOF의 의미

EOF란 문자가 아니다.

텍스트 파일에서 데이터는 ASCII 코드 값 형태로 저장된다.

ASCII 코드 값의 범위는 0~127이고, -1은 불가능하므로 EOF(-1)을 파일 끝 표시로 사용할 뿐

파일에 실제로 존재하는 것이 아니다.

EOF는 읽기 파일이 끝에 도달했음, 또는 I/O 작업에서 읽기 및 쓰기 오류가 발생했음을 나타낸다.

<br>

# EOF의 목적과 사용

입력이 끝났을 때 프로그램을 종료한다는 점에 착안해 

이를 이용해서 백준 풀이 시 적당히 입력받고 종료하기 위한 프로그램을 작성한 것이지,

나는 에러에 대처하려고 사용한 것이 아니다.

때문에 "vs 2015 버전 업데이트 후에 ctrl + z를 여러 번 입력해야 종료되요~" 는

'미정의 동작'은 아닌 것으로 보인다.

<br>

# 그래서 원인은?

사실 정확한 원인은 내가 구조를 뜯어볼 능력도 부족하고

기존 질문 답변을 봐도 이해하지 못했다.

CRT(C Runtime) 내 버퍼를 처리하는 구현의 이슈로 추정되며 여러모로 추측만 가득하다.


<br>

# 결론

while (cin >> n) {...} 을 사용하자 !


<br>

# 예제

eof 사용법을 익혀

아래와 같은 문제에 사용해보자.

<https://www.acmicpc.net/problem/11718>

<https://www.acmicpc.net/problem/10951>

<br>

# 참고 링크

vs 포럼

<https://social.msdn.microsoft.com/Forums/vstudio/en-US/3c07e114-0b8f-45e8-8082-bf42ac1409ca/a-question-about-how-scanf-works?forum=vcgeneral>


stackoverflow 질문

<https://stackoverflow.com/questions/39711028/undefined-behaviour-of-console-application-when-using-scanf-and-simulated-eof>

<https://stackoverflow.com/questions/33059976/why-do-i-have-to-type-ctrl-z-3-times-to-send-eof>


EOF 백준

<https://www.acmicpc.net/board/view/45412>


csdn eof 의미

<https://blog.csdn.net/henu1710252658/article/details/83040281>

<https://blog.csdn.net/leslietuang/article/details/17095233?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-17095233-blog-104175018.pc_relevant_downloadblacklistv1&spm=1001.2101.3001.4242.4&utm_relevant_index=8>


프갤 답변

<https://gall.dcinside.com/board/view/?id=programming&no=841002>

