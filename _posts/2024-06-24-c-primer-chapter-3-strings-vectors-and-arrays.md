---
layout: post
title: "[C++ Primer] Chapter 3 Strings, Vectors and Arrays"
category: [C++]
date: 2024-06-24 18:30:00 +0900
tag: [C++, book]
description: summary of C++ Primer chapter 3
comments: false
---

- 이 장에서는 `vector`와 `string`라이브러리에 대해 알아본다.

## 3.1 네임스페이스 `using` 선언

- `std::cin`에서 `::`은 왼쪽 파연산자의 유효범위에서 오른쪽 피연산자인 이름을 찾으라는 것이다.
- `using`을 쓰면 접두어로 이름을 한정 짓지 않고도 네임스페이스에 있는 이름을 알 수 있다.
- `using` 선언은 이름마다 따로 해야 한다
  - `using`선언을 한줄에 여러개 넣을 수도 있다.
  - 사용하는 이름별로 `using`선언을 해야하고 각 `using`선언을 세미콜론으로 마쳐야 한다.
- 헤더에는 `using` 선언을 포함하지 않는다.
  - 안 쓰는 것이 좋다. ← 특정 라이브러리 이름을 사용할 의도가 없는 프로그램에서 생각하지 못한 이름 충돌이 생길 수 있다.

## 3.2 `string` 라이브러리 타입

- `string`은 가변 길이 문자열이다.
- `#include <string>`와 `using std::string;` 을 해줘야 쓸 수 있다.

### 3.2.1 `string` 정의와 초기화하기

```cpp
string s1;
string s2 = s1;
string s3 = "hiya";
string s4(10, 'c'); // c가 10개
```

- 직접 초기화와 복사 초기화
  - `=`를 쓰면 복사 초기화 ← 오른쪽 피연산자인 초기값을 복사해 새로 만드는 객체에 넣도록 한다.
  - `=`를 안쓰면 직접 초기화
  - 초기값이 하나이면 직접이나 복사 초기화를 써도 좋다. 하지만 초기값이 여럿이면 반드시 직접 초기화 형식을 써야한다.

### 3.2.2 `string`연산

- 클래스에선느 객체를 만들고 초기화하는 방법고 함께 해당 클래스 타입 객체로 수행할 수 있는 연산도 정의한다.
- `string` 읽고 쓰기
  - `string`입력 연산자는 빈칸, 줄바꿈, 탭 등 앞에 나오는 공백 문자는 읽은 후 버리고, 다음 공백 문자가 나올때까지 문자를 읽는다.
  - 여러 입력 또는 출력을 연달아 쓸 수 있다.

```cpp
getline(is, s) // is에서 한줄을 읽고 s에 넣고 is를 반환한다.
s.empty()      // s가 비어있다면 true 아니면 false를 반환한다.
s.size()       // s의 문자 수를 반환한다
s[n]           // s에서 n번째 char에 대한 참조자를 반환한다.
s1 + s2        // 두 문자열을 결합한 문자열을 반환한다.
s1 = s2        // s1의 문자를 s2의 복사본으로 바꾼다.
s1 == s2       // 비교한다.
s1 != s2       // 상등 비교는 대소문자를 구별한다.
<, <=, >, >=   // 비교는 대소문자를 구별하여 사전 순으로 한다.
```

- 임의의 개수 `string`읽기
- `getline`을 사용해 한 줄 전체 읽기
  - 입력에서 공백 문자를 무시하지 않았으면 할 때가 있다
  - 지정한 스트림에서 줄바꿈 문자를 만날 때까지, 줄바꿈 문자를 포함해 입력 내용을 읽고 그 줄바꿈 문자를 **제외**한 내용을 인자로 지정한 `string`에 저장한다.
- `string empty`와 `size`연산
  - `size`멤버에서는 `string`의 길이, 즉 `string`의 문자 수를 반환한다.
- `string::size_type` 타입
  - `size`가 반환하는 타입은 `string::size_type`이다.
- `string`비교하기\
  - 두 `string`의 길이가 다르고 짧은 `string`의 모든 문자가 긴 것의 같은 위치에 있는 문자와 같다면 짧은 것이 긴 것 보다 작다.
  - 두 `string`에서 대응하는 위치의 어떤 문자가 서로 다를 때 비교 결과는 `string`이 다른 첫번째 문자 비교 결과에 따른다.

```cpp
string str = "Hello";
string phrase = "Hello World";
string slag = "Hiya";
str < phrase < slag
```

- `string` 대입
  - 대입이 가능하다
- 두 `string` 더하기
  - 왼쪽 피연산자의 문자 복삽존 뒤에 오른쪽 피연산자의 문자 복사본을 붙인 새로운 `string`을 반환한다.
- 상수와 `string` 덧셈
  - 문자 산수와 문자열 상수 모두를 `string`으로 변환할 수 있다.
  - `string`을 문자 상수나 문자 상수와 함께 쓸 때는 `+` 연산자의 피연산자 중 하나는 `string`타입이어야 한다.

### 3.2.3 `string` 내 문자 다루기

- C헤더 이름은 `<name.h>`이고 C++ 헤더의 이름은 `<cname>`이다. C++ 버전을 사용하는 것이 더 좋다.
- 모든 문자를 처리하려면? 범위 기반 `for`를 사용한다.
  - 아래 코드와 같이 `str`의 모든 문자를 출력할 수 있다.

```cpp
for (auto c : str)
    cout << c << endl;
```

- 범위 `for`를 사용해 `string`내 문자 변경하기
  - `string`내 문자 값을 변경하려면 루프 변수를 참조자 타입으로 정의해야 한다.
- 일부 문자만 처리하려면?
  - 첨자 연산을 사용해서 접근할 수 있다. 첨자 연산자 안에는 정수 값을 반환하는 타입이면 모두 쓸 수 잇다. `s[0]`
- 반복에 첨자 사용하기
  - `for`문과 첨자를 사용해 `string`을 순회할 수 있다.
- 첨자를 사용해 임의 접근할 수 있다.

## 3.3 `vector` 라이브러리 타입

- `vector`는 타입이 모두 같은 객체의 모음이다. 흔히 컨테이너라고 한다.
- `include<vector>`와 `using std::vector;`를 써야한다.
- `vector`는 클래스 템플릿이다.
- 컴파일러에서 템블릭을 사용해 클래스나 함수를 만드는 과정은 인스턴스화 라고 한다.
- 클래스 템플릿인 경우 추가 정보를 사용해 인스턴스로 만들 클래스를 지정하는데 이 정보 특성은 템플릿에 의존한다. `vector<int>`와 같이 꺾쇠 안에 넣는다.
- `vector`에 담을 객체 타입은 거의 대부분의 타입을 쓸 수 있다.

### 3.3.1 `vector`의 정의와 초기화하기

```cpp
vector<string> = svec;
vector<int> ivec;
vector<int> ivec2(ivec); // ivec을 복사해서 ivec2에 넣는다.
```

- `vector`를 목록 초기화하기
  - `vector<string> articles = {"a", "asdf"};`와 같이 하거나 `vector<string> v1{"a", "asdf"};`로 초기화를 할 수 있다.
- 값 초기화
  - 아래 초기화 방식에는 두가지 제약이 있다.
    - 일부 클래스에서는 항상 명시적으로 초기값을 지정해야 한다.
    - 초기 값 없이 요소 개수를 지정할 때는 꼭 직접 초기화 형식을 써야한다.

```cpp
vector<int> ivec(10);
vector<string> svec(10);
```

- 목록 초기 값 또는 요소 개수
  - 괄호를 이용한 초기화는 객체를 생성하는 데 지정한 값을 사용한다는 뜻이다.
  - 중괄호는 객체를 목록 초기화할 수 있으면 그렇게 하겠다는 뜻이다.

### 3.3.2 `vector`에 요소 추가하기

- `push_back`을 사용하면 벡터의 맨 마지막에 새로운 요소를 넣을 수 있다.
- `vector`는 효율적으로 커지기 때문에 처음에 크기를 정하지 않는 것이 더 좋다.
- `vector`에 요소를 추가하는 것에 내포된 의미를 프로그래밍하기
  - 루프 본체에서 `vector`에 요소를 추가한다면 범위 `for`는 사용할 수 없다.

### 3.3.3 다른 `vector`연산

- `vector`도 `string`과 유사하게 작동한다.
- `vector` 색인 계산하기
  - 색인을 계산해서 `vector`에 접근할 수 있다.
- 첨자 연산을 요소를 추가하지 않는다.
  - 파이썬의 딕셔너리에 요소 추가하는 것 처럼 없는 인덱스에 값을 대입하면 안된다.

## 3.4 반복자 소개

### 3.4.1 반복자 사용하기

- `begin`멤버는 첫 번째 요소를 나타내는 반복자를 반환한다.
- `end`에서 반환한 반복자는 연관된 컨테이너의 마지막 요소 바로 다음에 위치한 반복자이다.
- 일반적으로 정확한 반복자 타입은 모른다. `auto`를 쓰면된다.
- 반복자 연산
  - 역참조를 통해 반복자가 나타내는 요소를 얻을 수 있다.
- 반복자 이동하기
  - 증가 연산자`++`를 통해 반복자를 다음 요소로 옮길 수 있다.
- 반복자 타입

```cpp
vector<int>::iterator it;
vector<int>::const_iterator it3;
```

- `begin`과 `end`연산
  - 연산 대상 객체가 `const`이면 `const_iterator`를 반환한다.
  - `cbegin`과 `cend`는 무조건 `const_iterator`를 반환한다.
- 역참조와 멤버 접근 결합하기
  - `it`가 벡터에 속한 반복자라면 `it`로 난타내는 `string`이 비었는지 확인 → `(*it).empty()`
  - 혹은 화살표 연산자를 이용해 `it->empty()`로 나타낼 수도 있다.
- 일부 `vector` 연산은 반복자를 무효화한다.
  - `for`루프 안에서 `push_back`을 하면 반복자를 무효화한다.

### 3.4.2 반복자 산술 연산

- `string`과 `vector`에 대한 반복자에서는 한번에 여러 요솔르 이동하는 연산도 할 수 있으며 모든 관계 연산자도 지원한다. → 이런 연산을 반복자 산술 연산이라고 한다.
- 반복자에서 산술 연산
  - 정수 값을 복자와 더하거나 뺄 수 있는데, 그렇게 하면 여러 요소를 앞으로 또는 뒤로 이동한 위치의 반복자를 반환한다.
  - 관계 연산자를 이용해 `vector`와 `string`을 비교할 수 있다.
  - 두 반복자 간의 뺄셈도 가능하며 이는 `dirrerence_type`을 반환한다.

## 3.5 배열

- 배열은 크기가 고정되어 있어서 배열에 요소를 추가할 수 없다. 이는 유용성을 희생한 결과이다.

### 3.5.1 내장 타입 정의와 초기화하기

- 배열은 `a[d]`형태로 선언하고 `d`는 상수어이야한다.
- 배열을 정의할 때에는 배열 타입을 지정해야하며, `auto`를 쓸 수 없다. 참조자의 배열은 없다
- 배열 요소를 명시적으로 초기화하기
  - 배열 요소를 목록 초기화할 수 있으며 이때는 차원을 생략할 수 있다.
  - 차원이 초가ㅣ 값 수보다 크면 첫 요소부터 차례로 초기값을 사용해 초기화하고 남은 요소는 값 초기화한다.
- 문자 배열을 특별하다.
  - 문자열 배열은 문자열 상수를 활용새 초기화할 수도 있다.
  - 널문자도 같이 복사되므로 배열의 크기가 최소 문자열의 길이보다 1 커야 한다.
- 복사와 대입 금지
  - 배열은 다른 배열의 복사본으로 초기화할 수 없을 뿐만 아니라 배열을 다른 배열에 대입하는 것도 안된다.
- 복잡한 배열 선언 이해하기

```cpp
int *ptrs[10];
int &refs[10] = // 오류 참조자의 배열은 없다
int (*Parray)[10] = &arr;
int (&arrRef)[10] = arr;
```

### 3.5.2 배열 요소에 접근하기

- 배열 요소에 접근할 때도 범위 `for`나 첨자 연산자를 쓸 수 있다.
- 배열 첨자로 변수를 사용한다면 보통 그 변수는 `size_t` 타입으로 정의하는 것이 좋다. `cstddef` 헤더의 정의되어있다.
- 첨자 값 확인하기
  - 배열의 크기가 넘어가도록 첨자를 써도 프로그램은 멈추지 않는다. 치명적인 문제가 생기므로 쓰지 않는 것이 좋다

### 3.5.3 포인터와 배열

```cpp
string *p2 = nums; // p2 = &nums[0]과 같다
```

- 포인터는 반복자이다.
  - 포인터도 증감 연산을 통해 반복자처럼 사용할 수 있다.
- `begin`과 `end`라이브러리 함수
  - `iterator`헤더에 있는 `begin`함수는 배열의 맨 처음 포인터를 반환하고, `end`함수는 배열의 맨 마지막 다음 포인터를 반환한다.
- 포인터 산술 연산
  - 배열 요소를 가리키는 포인터에서는 모든 반복자 연산을 사용할 수 있다.
  - 정수 값을 더하거나 빼면 새로운 포인터 값을 얻는다.
  - 두 포인터를 뺀 결과는 `ptrdurr_t`라이브러리 타입을 반환한다. `cstddef`헤더에서 정의한다.
- 역참조와 포인터 산술 연산 사이의 상호작용
  - `int last = *(ia + 4);`이 코드는 `ia`의 4번째 값을 구한다.
- 첨자와 포인터
  - 대부분의 배열 이름을 쓰면 실제로는 그배열의 첫 요소에 대한 포인터를 사용한다.

### 3.5.4  C 형식 문자열

- 문자열 상수는 C++에서 C로부터 물려받은 더 일반적인 구문의 한 예이며 C 형식 문자열이라고 한다.
- 이 규약을 따르는 배열은 문자 배열에 저장하고 널 종료한다. ← 마지막 문자가 널 문자이다.
- C 라이브러리 문자열 함수
  - 이러한 함수들은 무조건 마지막이 널인 문자열에 사용해야 한다
- 문자열 비교하기
  - 포인터 값이 아니라 문자열을 비교하려면 `strcmp`를 호출해야 한다.
- 목적지 문자열의 크기는 호출하는 쪽에서 책임진다
  - C 형식 문자열보다 `string`라이브러리를 사용하는 것이 더 안전하고 더욱 효율적이다.

### 3.5.5 오래된 코드와 함께 쓰기

- 오래된 C++ 프로그램은 표준 라이브러리 이전에 만들어졌다. → 최신 C++로 만들 프로그램을 배열과 C형식 문자열을 사용하는 코드와 함께 써야 할 수도 있다. C++ 라이브러리에서는 함께 쓰기 더 쉽도록 여러 기능을 제공한다.
- `string`라이브러리와 C 형식 문자열 함께 쓰기
  - 문자열 상수를 쓸 수 있는 곳은 모두 널 종료 문자 배열을 사용할 수 있다.
  - 문자열 포인터를 `string`으로 초기화할 방법 중 하나는 `string`멤버 함수인 `c_str`를 쓰는 것이다.
- 배열을 사용해 `vector`초기화하기

```cpp
int int_arr[] = {0, 1, 2, 3, 4, 5};
vector<int> ivec(begin(int_arr), end(int_err));
vector<int> subVec(int_arr+1, int_arr+4);
```

- 포인터와 배열은 오류가 생기기 쉽다. 최신 C++ 프로그램에서는 내장 배열과 포인터 대신 `vector` 와 반복자를, C 형식 배열 기반 문자열보다 `string`을 쓰는 것이 좋다.

## 3.6 다차원 배열

- 엄격히 말해 C++에는 다차원 배열이 없다. 일반적으로 다차원 배열은 배열의 배열이다.
- 2차원 배열에서 첫 번째 차원은 일반적으로 행, 두번째는 열을 나타낸다.
- 다차원 배열 요소 초기화하기
  - C와 비슷한 방식으로 초기화 가능하다.
- 다차원 배열 첨자 연산하기
  - 표현식에서 첨자 수를 차원만큼 사용하면 지정한 타입인 요소를 얻지만 첨자 수가 차원보다 적으면 지정한 색인에 위치한 내부 배열 요소를 결과로 얻는다.
- 다차원 배열에 범위 `for`사용하기
  - 다차원 배열을 범위 `for`에서 쓰려면 가장 안쪽 배열을 제외한 모든 루프 제어 변수를 참조자로 해야한다.
- 포인터와 다차원 배열
  - 다차원 배열도 이름을 사용하면 자동으로 해당 배열의 첫 요소에 대한 포인터로 변환한다.
- 타입 별칭을 사용하면 다차원 배열에 대한 포인터를 간단히 할 수 있다.
