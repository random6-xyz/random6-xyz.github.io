---
layout: post
title: "[C++ Primer] Chapter 6 Functions"
category: [C++]
date: 2024-06-29 23:39:00 +0900
tag: [C++, book]
description: summary of C++ Primer chapter 6
comments: false
---

- 함수는 이름이 있는 구역이며, 이 함수를 호출해 코드를 실행한다.

## 6.1 함수 기초

- 함수 정의는 기본적으로 반환이나 타입, 이름, 없거나 하나 이상인 매개변수 목록, 본체로 구성한다.
- 함수는 괄호로 쌓인 호출 연산자를 통해 실행한느데 이 연산자에서는 함수나 함수에 대한 포인터인 표현식을 취한다.
- 함수 만들기 및 호출하기

```cpp
int fact(int val) {
    int ret = 1;
    return ret;
}

fact(1);
```

- 함수 호출에서 하는 일
  - 해당 인자를 사용해 함수 매개변수를 초기화하고 제어를 그 함수로 옮긴다.
  - 호출하는 함수의 실행을 잠시 멈추고 호출되는 함수의 실행을 시작한다.
- `return`문을 만나면 하는 일
  - 값이 있으면 그 값을 반환하고 호출된 함수에서 호출한 함수로 제어를 다시 옮긴다.
- 매개 변수와 인자
  - 인자는 함수 매개변수에 대한 초기값이다. 인자를 평가하는 순서는 보장하지 않는다. 컴파일러에 따라 다르다.
- 함수 매개변수 목록
  - 함수 매개변수 목록은 비어있을 수는 있지만 생략할 수 는 없다. `int func(void) {}`로도 쓸 수 있다.
  - 두 매개변수 이름이 같을 수는 없다. 함수의 가장 바깥 유효범위에 있는 지역변순느 매개변수와 이름이 달라야한다.
  - 매개변수의 이름은 선택적지만 이름이 없는 매개변수를 사용할 방법은 없다.
- 함수 반환 타입
  - `void`타입을 포함한 대부분의 타입을 사용할 수 있다.
  - 배열 타입이나 함수 타입은 반환 타입으로 쓸 수 없다. ← 이를 배열 또는 함수에 대한 포인터를 반환할 수 있다.

### 6.1.1 지역 객체

- 유효범위 - 프로그램 본문에서 해당 이름을 볼 수 있는 부분이다
- 객체의 수명 - 프로그램을 실행하는 동안 객체가 존재하는 시간이다.
- 함수 본체 안에서 정의한 매개변수는 변수를 지역변수라고 한다.
- 모든 함수 밖에서 정의한 객체는 프로그램을 실행하는 동안 내내 존재한다.
- 자동 객체
  - 구역을 실행하는 동안에만 존재하는 객체
  - 매개변수도 포함된다.
- 지역 `static` 객체
  - 수명이 함수 호출을 너머 지속하는 지역변수
  - 초기값이 없으면 0으로 만든다.

### 6.1.2 함수 선언

- 함수를 결코 선언하지 않는 한, 그 함수를 정의하지 않아도 선언할 수 있다. → 나중에 다룬다.
- 매개변수 이름은 없어도 된다.
- 함수 선언은 함수 원형이라고도 한다.
- 함수 선언은  헤더 파일에 둔다
  - 선언은 헤더 파일에 두고 정의는 소스 파일에 하는 것이 좋다

### 6.1.3 분리 컴파일

- 여러 소스 파일을 컴파일과 링크하기
  - `c` 옵션을 통해 오브게트 파일을 만들 수 있다. 이 오프젝트 파일을 이용해서 실행파일을 만든다.

## 6.2 인자 전달

- 매개변수가 참조자이면 해당 인자를 **참조로 전달**이라고 하거나 함수를 참조로 호출한다고 한다.
- 인자 값을 복사할 때 매개변수와 인자는 독립적인 객체이다. 이런 인자를 **값으로 전달**한다고 하거나 다른 말로 그 함수를 값으로 호출한다고 한다.

### 6.2.1 값에 의한 인자 전달

- 값으로 인자를 전달하면 원래 변수에 영향을 미칠 수 없다.
- 포인터 매개변수
  - 포인터는 비참조자 타입처럼 행동한다.
  - 일반적으로 C에서는 포인터 매개변수를 사용해 함수 외부 객체에 접근한다. C++에서는 그 대신 참조자 매개변수를 사용한다.

### 6.2.2 참조자로 인자 전달

- 매개변수는 종종 함수에서 인자 값 하나 이상을 변경하는데 사용한다.
- 참조자를 사용해 복사 피하기
  - 크기가 큰 클래스 타입이나 컨테이너 객체를 복사하는 것은 비효율적일 수 있다. 그대서 참조자를 사용해 이를 피할 수 있다.
  - 함수 내에서 변경하지 않는 참조자 매개변수는 `const`에 대한 참조자여야 한다.
- 참조자 매개변수를 사용해 추가 정보 반환하기
  - 함수에서는 값을 단 하나만 반환할 수 있다. 하지만 하나 이상을 반환해야할 때도 있다. → 참조자 매개변수를 사용하면 된다.

### 6.2.3 `const`매개변수와 인자

- 상위 `const`인 매개변수에 `const`와 `const`가 아닌 객체 어느 것이든 전달할 수 있다.
- 포인터 또는 참조자 매개변수와 `const`
- 매개변수는 변수 초기화와 같은 방식으로 초기화하므로 일반적인 초기화 규칙을 적용하면 된다.
- 가능하면 `const`에 대한 참조자를 사용한다.

### 6.2.4 배열 매개변수

- 배열은 복사할 수 없으며 배열을 사용할 때 그 배열은 (일반적으로) 포인터로 변환한다
- 함수에 배열을 전달할 때 실제로는 해당 배열의 첫 요소에 대한 포인터를 전달한다.
- `const int*`하나의 타입만 존재한다.
- 표시자를 사용한 배열 범위 지정하기
  - 배열 자체에 끝을 나타내는 표시자를 포함하는 방법
- 표준 라이브러리 변환 사용하기
  - 배열의 첫 요소와 마지막 요소 바로 다음에 대한 포인터를 전달하는 것이다.
- 배열 매개변수와 `const`
  - 함수에서 요소 값을 변경해야할 경우에만 매개변수를 `const`가 아닌 타입에 대한 보통의 포인터로 사용해야 한다.
- 배열 참조자 매개변수
  - 매개변수도 배열에 대한 참조로 정의할 수 있다.
  - `void print(int (&arr)[10])`로 선언하면 된다.
- 다차원 배열 전달하기
  - 다차원 배열 역시 첫 요소에 대한 포인터로 전달한다.
  - 두번째 이하의 차원 크기는 해당 요소 타입의 일부분이므로 반드시 지정해야 한다.
  - 배열 문법을 사용해 함수를 정의할 수도 있는데, 일반적으로 컴파일러에서는 첫 번째 차원을 무시하므로 포함하지 않는 것이 좋다.

### 6.2.5 `main` : 명령행 옵션 처리하기

- `int main(int argc, char **argv) {}`
- 인자를 `main`에 전달하면 `argv`의 첫 요소에서는 프로그램 이름이나 빈 문자열을 가리킨다. 그 이하 요소는 명령행에서 제공한 인자를 전달하면 마지막 포인터 바로 다음 요소는 0임을 보장한다.

### 6.2.6 매개변수가 가변인 함수

- 가변 인자 수를 취하는 함수를 만들기 위한 두가지 기본적인 방법
  - 모든 인자 타입이 같으면 `initializer_list` 라이브러리 타입을 전달할 수 있다.
  - 인자 타입이 다양하면 가변인자 템플릿이라고 하는 특별한 함수를 만들 수 있다.
  - 개수가 가변인 인자를 전달하는 데 상요할 숭 씨는 특별한 매개변수 타입인 매개변수 생략도 있다. → 이 방법은 프로그램에서 C함수와 인터페이스할 때만 사용하는것이 좋다.
- `initializer_list`매개변수
  - 이 요소는 항상 `const`이므로 요소값을 변경할 수 없다.
  - `void error_msg(initializer_list<string> il) {}`와 같이 사용한다.
- 매개변수 생략
  - C 라이브러리인 `varargs`를 사용하는 C코드와 프로그램을 인터페이스할 수 있다.
  - `void foo(parm_list, ...); void foo(...)`로 쓴다.

## 6.3 반환 타입과 `return`문

### 6.3.1 반환 값이 없는 함수

- `void`타입의 함수에서만 사용할 수 있다.

### 6.3.2 값을 반환하는 함수

- 반환 값은 함수 반환 타입과 타입이 같거나 그 타입으로 암시적 변환을 할 수 있어야 한다.
- 값을 반환하는 법
  - 값은 변수와 매개변수를 초기화하는 것과 정확히 같은 방식으로 반환한다.
- 지역 객체에 대한 참조자나 포인터는 절대 반환하지 않는다
  - 지역객체에 대한 포인터를 반환하는 것도 역시 잘못이다.
- 클래스 타입을 반환하는 함수와 호출 연산자
  - 호출 연산자 역시 결합법칙과 우선순위를 따른다. 호출 연산자는 점, 화살표연산자와 우선순위가 같고 이 연산자와 마찬가지로 왼쪽 결합이다.
- 참조자 반환은 좌변 값이다
  - 참조자를 반환하는 함수에 대한 호출은 좌변 값이지만 다른 반환 타입은 우변 값을 반환한다.
  - 이런 것도 가능하다.

```cpp
char &get_val() {
   return 'a';
}

get_val() = 'A';
```

- 반환 값 목록 초기화
  - 중괄호로 둘러싼 값 목록을 함수에서 반환할 수 있다.
  - 함수 반환을 나타내는 임시 객체를 초기화할 수 있다.
- `main`에서 반환
  - `main`함수에서는 반환하지 않고 종료할 수 있다. 컴파일러가 자동으로 추가한다.
  - 반환한 값은 상태 표시자로 취급한다. `cstdlib`헤더에서 성공과 실패를 나타내는 데 사용할 수 있는 전처리기 변수를 정의한다.
- 재귀
  - 직간접적으로 자신을 호출하는 함수를 재귀함수라고 한다.
  - `main`함수에서는 자신을 호출할 수 없다.

### 6.3.3 배열에 대한 포인터 반환하기

- 함수에서는 배열 자체는 반환할 수 없지만 배열에 대한 포인터나 참조자는 반환할 수있다.
- `typedef int arrT[10]` - 타입별칭을 통해 함수 선언을 간단히 할 수 있다.
- 배열에 대한 포인터를 반환하는 함수 선언하기
  - 타입 별칭을 사용하지 않고 `func`을 선언하려면 정의하는 이름 뒤에 밴열 차원이 있어야 한다.
  - `타입 (*함수(매개변수_목록)) [차원]` - 이렇게 쓰면된다.
- 후행 반환 타입
  - 후행 반환 타입은 매개변수 목록 다음에 오고, 이 앞에는 `->`를 둔다.
  - 일반적으로 반환 타입을 두는 곳에 `auto`를 둔다.
  - `auto func(int i) → int(*)[10];`
- `decltype`사용하기
  - 함수에서 반환하는 포인터에서 가리킴는 배열을 알 수 있으면 `decltype`을 사용해 반환 타입을 선언할 수 있다.

```cpp
int asdf[] = {1,2,3,4,5};
decltype(asdf) *arrPtr(int i) {}
```

## 6.4 함수 다중 정의

- 이름은 같지만 매개변수가 다르며 같은 유효 범위 내에 있는 함수를 다중 정의했다고 한다.
- 이 함수를 호출할 때 컴파일러에서는 전달하는 인자 타입을 바탕으로 원하는 함수를 유추할 수 있다.
- `main`함수는 다중 정의가 불가하다.
- 다중 정의한 함수 정의하기
  - 두 함수에서 반환 타입만 다르다면 오류이다.
- 두 매개변수 타입이 다른지 결정하기
- 다중 정의와 `const`매개변수
  - 하위 `const`처럼 매개변수가 해당 타입의 `const`나 `const`가 아닌 버전에 대한 참조자나 포인터인지 여부를 바탕으로 다중 정의 가능하다.
- `const_cast`와 다중 정의
- 다중 정의한 함수 호출하기
  - 함수 일치는 다중 정의한 함수 집합에서 특정한 함수 호출을 특정 함수와 연관 짓는 과정이다.

### 6.4.1 다중 정의와 유효 범위

- 일반적으로 내부 유효 범위에 이름을 선언함녀 그 이름은 외부 유효 범위에 선언한 이름을 가려 사용하지 못하게 한다. 이름은 유효 범위를 가로질러 다중 정의하지 않는다.

## 6.5 전문적 용도를 위한 기능

- 유용한 세가지 함수 관련 기능인 기본 인자, 인라인, `constexpr`함수를 다루고 디버깅할 때 자주 사용하는 일부 기능을 다룬다.

### 6.5.1 기본인자

- 매개변수의 공통 값을 함수에 대한 기본 인자로 선언할 수 있다.
- 그 인자를 사용하거나 사용하지 않고 호출할 수 있다.
- 매개변수 하나 이상에 대해 기본 값을 정의할 수 있지만 매개변수에 기본인자를 지정하면 그 매개변수 뒤에 오는 모든 매개변수에도 기본 인자를 지정해야 한다.
- 기본 인자를 사용해 함수 호출하기
  - 기본 인자를 사용하려면 함수를 호출할 때 해당 인자를 생략하면 된다.
  - 호출에서 인자는 위치로 해석한다. 기본인자는 가장 후행에서 취급한다.
- 기본 인자 선언
  - 헤더에서 함수를 한 번 선언하는 것이 일반적인 관례이지만 함수를 여러 번 재선언해도 괜찮다.
  - 해당 유효범위 안에서 각 매개변수에는 기본 값을 한 번만 지정할 수 있다.
- 기본 인자 초기화식
  - 지역 변수는 기본 인자로 사용할 수 없다. 이런 제약을 제외하고 해당 매개변수 타입으로 변환할 수 있는 모든 표현식은 기본 인자로 사용할 수 있다.

### 6.5.2 인라인과 `constexpr`함수

- 함수 호출은 그냥 표현식 보다 더 많은 리소스를 잡아먹는다.
- `inline`함수를 사용해 함수 호출에 추가 부담을 피한다
  - `inline`으로 정의한 함수는 일반적으로 호출한 각 위치에 '정렬해' 확장한다.
  - 일반적으로 `inline`매커니즘에서의도한 것은 자주 호출하는 작고 직선적인 함수에 대한 최적화이다.
- `constexpr`함수
  - 상수 표현식에 사용할 수 있는 함수이다.
  - 조건 - `return`타입과 각 매개변수 타입이 상수 타입이어야 하고 함수 본체에는 `return`문이 정확히 하나만 있어야 한다.
  - 상수 표현식을 반환해야 하는 것은 아니다.

### 6.5.3 오류 수정 지원 도구

- `assert`전처리기 매크로
  - 전처리기 매크로는 어느 정도 인라인 함수처럼 행동하는 전처리기 변수이다.
  - `assert (표현식);`
  - 0이면 에러 메세지를 출력하고 프로그램을 종료한다.
- `NDEBUG`전처리기 변수
  - `NDEBUG`를 정의하면 `assert`에서는 아무것도 하지 않는다.
  - `define`또는 명령행 옵션을 사용해 활성화 시킬 수 있다.

## 6.6 함수 일치

- 후보와 호출 가능 함수 결정하기
  - 후보 함수 - 함수 일치 첫 단게에서는 호출을 고려할 수 있는 다중 정의한 함수 집합이다. 이게 함수 집합이 후보 함수이다.
  - 주어진 호출에서 사용한 인자로 호출할 수 있는 함수를 후보 함수 집합에서 선택한다. 이렇게 선택한 함수가 호출 가능 함수이다.
- 가장 일치하는 것(이 있다면) 찾기
  - 함수 기능 함수 중 어느 것이 해당 호출과 가장 일치하는지 결정한다.
- 여러 매개변수와 일치하는 함수
  - 이 경우 컴파일러가 불평한다.

### 6.6.1 인자 타입 변환

- 가장 일치하는 것을 결정하기 위해 컴파일러에서는 각 인자를 해당 매개변수 타입으로 변환하는 데 사용할 수 있는 변환에 순위를 매긴다.
  - 정확한 일치
  - `const`변환을 통한 일치
  - 승격을 통한 일치
  - 산술 또는 포인터 변환을 통한 일치
  - 클래스 타입 변환을 통한 일치
- 승격 또는 산술 변환을 필요로 하는 일치
- 함수 일치와 `const`인자

## 6.7 함수에 대한 포인터

- 함수 포인터는 단지 객체 대신 함수를 나타내는 포인터이다.
- 함수 타입은 반환 타입과 매개변수 타입으로 결정하며 함수 이름은 타입에 속하지 않는다.
- 함수 포인터 사용하기
  - 함수 이름을 값으로 사용하면 그 함수를 자동으로 포인터로 변환한다. → 이를 통해 호출할 수 있다.
  - `nullptr`이나 0을 넣어서 아무 함수도 가리키지 않는다는 것을 나타낼 수 있다.
- 다중 정의한 함수에 대한 포인터
  - 포인터 타입을 사용해 다중 정의한 함수 중 어는 것을 사용할지 결정한다.
- 함수 포인터 매개변수
  - 배열과 마찬가지로 함수 타입 매개변수는 정의할 수 없지만 함수에 대한 포인터를 매개변수로 할 수는 있다.
- 함수에 대한 포인터 반환하기
  - 배열과 마찬가지로 함수 타입을 반호나할  수는 없지만 함수 타입에 대한 포인터는 반환할 수 있다.
  - 타입 별칭을 사용하는 것이 가장 쉽다.
- 함수 포인터 타입에 `auto`나 `decltye`사용하기
  - 어느 함수를 반환해야 하는 하는지 알고 있다면 `decltype`을 사용해 함수 퐁니터 반환 타입을 간단히 만들 수 있다.
