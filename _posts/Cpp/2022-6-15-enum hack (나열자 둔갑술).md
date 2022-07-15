---
title: "enum hack (나열자 둔갑술)"
categories:	
    - Cpp
tags:
    - Cpp
---

Effective C++에서 소개하는 enum hack의 사용법과, 

내가 게임 만들 때 실습해본 enum hack 사례를 서술하려 한다.

<br>

# enum hack

나열자 둔갑술 기법.

나열자(enumerator)의 타입의 값은 int가 놓일 곳에도 쓸 수 있다는 점을 확용한 기법.

클래스 멤버 변수로 상수를 정의하는 경우 사용.

정수 타입이 정적 클래스 상수에 대한 클래스 내 초기화를 금지하는 구식 컴파일러에서 괜찮은 기법.

<br>

# 정적 멤버

클래스 멤버로 상수를 정의하는 경우,

어떤 상수의 유효범위를 클래스로 한정하고자 할 때는 그 상수를 멤버로 만들어야 하는데,

그 상수의 사본 개수가 한 개를 넘지 못하게 하고 싶다면 **정적(static) 멤버** 로 만들어야 한다.

```cpp
class Player
{
private:
	static const int maxEquipSlot = 5;
	int equipment[maxEquipSlot];
};
```

다만 선언 시점에 초기화를 진행하는 것을 허용하지 않는 구식 컴파일러에선 위와 같은 형태가 불가능하다.

또한 정적 클래스 멤버가 선언될 때 초기값 설정을 허용하지 않는다.

이때 클래스 상수의 선언은 헤더 파일에 두고, 정의는 구현 파일에 두는 방법도 있지만,

아래처럼 enum을 사용할 수 있다.

<br>

# enum

```cpp
class Player
{
private:
	enum { maxEquipSlot = 5 };
	int equipment[maxEquipSlot];
};
```

enum이 int가 놓일 곳에도 쓰일 수 있다는 점을 활용한 것이다.

이의 장점은,

1. 메모리 낭비가 없다.
2. 컴파일타임에 존재하므로 컴파일 에러 시 추적도 가능하다.
3. class 내부에 선언이 가능하기 때문에 객체지향적이다.


단점은, 정수형만 가능하다는 점이다.

<br>

# 사용 사례

Effective C++ 에서 읽은 내용을 토대로 게임에 접목시켜보았다.


```cpp
// 헤더
	class player final : public plane 
	{
	private:
		enum const_var_ {
			player_size,
			player_default_pos,
			player_default_frame,
			// ...생략
			player_bullet_max_num = 50
		};
		const std::vector<math::vec2i> coords_player_ = {
			{64, 58},		//player_size
			{320, 650},		//player_default_pos
			{64, 0},		//player_default_frame
			// ...생략
		};
	};
```
```cpp
// cpp
	void player::init() 
	{
		set_size(coords_player_[player_size]);
		set_frame_size(coords_player_[player_default_frame]);
		// ...생략
	}
```

위와 같이 x, y 좌표(매직넘버)를 나타내기 위해

클래스 헤더 파일에 enum을 전개했으며

사용할 때 배열 첨자 안에 enum의 어떤 값인지 가시화 해주고자 했다.

<br>

# enum class

다만 enum은 암시적 형 변환이 되니,

다른 enum 간 구분이 헷갈릴 수 있기 때문에

C++ 11에서 등장한 enum class를 사용하는 게 좋을 것이다.

```cpp
// 헤더
	enum class key_type_ 
	{
		none,
		arrow_up,
		arrow_left,
		arrow_down,
		arrow_right,
		space
	};
```
```cpp
// cpp
	void player::move(const float delta_time) {
		// ...생략
		set_pressed_key(static_cast<int>(key_type_::arrow_down));
	}
```

**형변환연산자(enum클래스명::값)**

과 같은 형태로 사용하도록 하자.

이제 다른 열거형과의 중복도 피할 수 있다.

<br>

# 결론

c++에서 매직 넘버를 사용할 때 enum class 를 사용하자.

1. 메모리 낭비 없음
2. 컴파일타임에 존재하여 디버깅 용이
3. 객체지향적 프로그래밍에 적합

단점
1. 정수형 상수만 가능


<br>

---


※ 더 좋은 방법이 있다면 가르쳐주시면 감사하겠습니다.