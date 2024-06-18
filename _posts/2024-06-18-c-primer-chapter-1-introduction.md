---
layout: post
title: "[C++ Primer] Chapter 1 Introduction\n"
category: [C++]
date: 2024-06-18 15:08:00 +0900
tag: [C++, book]
description: summary of C++ Primer chapter 1
comments: false
---

- 이 장에서는 타입, 변수, 표현식, 문장, 함수 등 C++의 기본 요소 대부분을 소개한다.
- 서점 프로그램을 만들 것이다.

## 1.1 간단한 C++ 프로그램 만들기

- `main` 이라는 이름의 함수는 꼭 존재해야 한다.
- OS가 `main`을 호출하고  C++ 프로그램을 실행한다.

```cpp
int main() {
    return 0;
}
```

- 함수 정의 4가지 요소
  - 반환 타입 - int 형이다. 0일 경우 성공을 나타내고 아니면 OS마다 다른 의미를 가지고 있다. -1일 경우에는 주로 실패를 뜻한다.
  - 함수 이름
  - 매개변수 목록
  - 함수 본체 - 중괄호를 통해 블럭을 나눈다.

### 1.1 프로그램을 컴파일하고 실행하기

- 소스 파일 - 프로그램 파일
  - 확장자는 .cc .cxx .cpp .cp .c  등이 쓰인다
- 소스 파일을 실행하는 방법을 알려준다. ~~알고 있기 때문에 패스~~
- 일반적으로 컴파일러에는 문제가 될 만한 구문을 경고로 표시하는 옵션이 있으며 이를 사용하는 것은 좋은 생각이다. `-Wall`, `/W4`를 쓰면 된다.

## 1.2 입출력 처음 살펴보기

- 표준 입출력 객체 - cin, cout, cerr, clog
- IO 라이브러리를 사용한 프로그램

```cpp
#include <iostream>
int main() {
    std::cout << "Enter two numbers: " << std::endl;
    int v1 = 0, v2 = 0;
    std::cout << "The sum of " << v1 << " and " << v2 << " is " << v1 + v2 << std::end1;
    return 0;
}
```

- 첫 줄은 컴파일러에게 `iostream` 라이브러리를 사용하겠다고 알리는 것으로 꺾쇠 괄호 안의 이름은 헤더를 나타낸다.
  - 라이브러리를 사용하는 모든 프로그램은 관련 헤더를 포함해야 하며 보통 시작 부분에 둔다.
- 스트림에 출력하기
  - `std::cout << "Enter two numbers: " << std::endl;`는 표현식을 실행한다. 표현식은 피연산자 하나 이상과 (흔히) 연산자 하나로 구성되며 결과를 만들어 낸다. 이 문장은 `<<`연산자를 통해 출력한다.
  - `<<`연산자는 피연산자를 2개 가지는데 왼쪽 피연산자는 `ostream`객체이어야 하고 오른쪽은 출력할 값이다. 이 연산자는 지정한 스트림에 지정한 값을 출력한다. 결과는 왼쪽에 있는 스트림이다. → 이를 통해 `<<`연산자를 연속해서 쓸 수 있다.
  - `std::cout << "Enter two numbers: "` - 오른쪽 메시지는 문자열인데 문자열이란 큰따옴표로 둘러싼 일련의 문지이다.
  - `std::cout << std::endl;` - 이 문장은 endl을 출력한다. 이 연산자는 조작자라는 특별한 값이다. 효과는 현재 줄을 마치고 버퍼를 비운다는 것이다. ← 버퍼는 꼭 비워야한다.
- 표준 라이브러리 이름 사용하기
  - 접두어 `std::`는 `cout`과 `endl`을 `std`라는 **네임스페이스** 안에 정의했음을 나타낸다.
  - 네임스페이스는 프로그래머가 우연히 라이브러리에서 정의한 것 같은 이름을 사용했을 때 발생하는 이름 충돌을 피하도록 해 준다.
  - 표준라이브러리에서 정의한 이름을 사용할 때는 그 이름이 `std`네임스페이스에 속한다는 것을 명시적으로 밝혀야 한다.
  - `::`는 범위 지정 연산자이다.

## 1.3 주석문에 대해

- 주석문 - 프로그래머가 프로그램을 읽는 데 도움을 주는 것 → 알고리즘 요약, 변수의 목적 밝히기, 명확히하기
- 주석의 종류
  - 한줄 주석문 - `//`
  - 쌍 주석문 - `/* */`
- 쌍 주석문은 중첩해서 쓸 수 없다.

## 1.4 제어 흐름

- 일반적으로 프로그램은 순차적으로 실행되지만 더 복잡한 실행 경로를 처리하도록 다양한 제어흐름을 제공한다.

### 1.4.1 `while`문

- `while`문은 지정한 조건이 참이 될 때까지 작은 구역을 반복해 실행한다.

```cpp
#include <iostream>

int main() {
    int sum = 0, val = 1;

    while (val <= 10) {
        sum += val;
        ++val;
    }
    std::cout << "Sum of 1 to 10 is " << sum << std::endl;
    
    return 0;
}

// while (조건) {
//     문장
// }
```

- 조건이 거짓일 때까지 (번갈아 가며) 조건을 확인하고 문장을 실행한다.
- 조건은 참 또는 거짓 중 하나를 결과로 반환하는 표현식이며 조건이 참일 동안 문장을 실행한다.
- 구역은 중괄호로 둘러싼 일련의 문장으로 구역안에 문장이 없을 수도 있다.

### 1.4.2 `for`문

- 조건에서 변수를 사용하고 그 변수를 본체에서 증가시키는 유형은 흔해서 `for`문이 만들어졌다.

```cpp
#include <iostream>

int main() {
    int sum = 0;
    
    for (int val = 1; val <= 10; ++val)
        sum += val;
    std::cout << "Sum of 1 to 10 is " << sum << std::endl;
    
    return 0;
}
```

- 헤더와 본체로 이루어진다.
  - 헤더는 초기문, 조건, 표현식으로 이루어짐

### 1.4.3 임의 개수 입력 읽기

```cpp
#include <iostream>

int main() {
    int sum = 0, value = 0;
    
    while (std::cin >> value)
        sum += value;
    std::cout << "Sum is " << sum << std::endl;

    return 0;
}
```

- 조건으로 istream을 사용하면 결과적으로 스트림 상태를 확인하는데 스트림이 유효하면 시험을 성공이다. 파일 끝에 도달하거나 잘못된 입력을 만나면 거짓을 반환한다.
  - 키보드 파일 끝 입력하기 - Ctrl+z(windows), Ctrl+d(unix)
- 컴파일러가 찾는 대표적인 오류
  - 문법 오류, 타입 오류, 선언오류

### 1.4.4 `if`문

```cpp
#include <iostream>

int main() {
    int currVal = 0, val = 0;
    if (std::cin >> currVal) {
        int cnt = 1;
        while (std::cin >> val) {
            if (val == currVal)
                ++cnt;
            else {
                std::cout << currVal << " occurs" << cnt << " times" << std::endl;
                currVal = val;
                cnt = 1;
            }
        }
        std::cout << currVal << " occurs " << cnt << " times" << std::endl;
    }
    return 0;
}
```

- C++ 프로그램에서 들여쓰기와 형식 맞추기
  - 형식이 매우 자유로우며 가독성이 좋게 일관되게 작성하는 것이 좋다.

## 1.5 클래스 소개

- C++ 에서는 클래스를 활용해서 데이터 구조를 정의한다.
- C++의 주된 설계관점은 내장 타입과 똑같이 행동하는 클래스 타입을 정의할 수 있게 하는 것이다.
- 클래스를 사용하려면 클래스의 이름, 정의한 곳, 할 수 있는 연산을 알아야한다.
- 여기서는 클래스 이름은 `Sales_itme`으로 하고 클래서는 `Sales_item.h`헤더에 정의한 것으로 한다.
- 클래스 제작자는 ㅇ치 클래스 객체로 할 수 있는 모든 행동을 정의한다.

### 1.5.1 `Sales_item`클래스

- 모든 클래스는 타입을 정의하며, 타입 이름은 클래스 이름과 같다.
- `Sales_itme item;`을 통해 `item`은 `Sales_item`타입 객체임을 알 수 있다.
- `Sales_item` 읽고 쓰기

```cpp
#include <iostream>
#include "Sales_item"

int main() {
    Sales_item book;
    std::cin >> book;
    std::cout << book << std::endl;
    return 0;
}
```

- 표준 라이브러리 헤더는 꺾쇠 괄호로, 비표준 라이브러리는 큰따옴표로 둘러싼다.
- `Sales_item` 더하기

```cpp
#include <iostream>
#include "Sales_item"

int main() {
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    std::cout << item1 + item2 << std::endl;
    return 0;
}
```

- 파일 방향 변경 사용하기

```shell
addItems <infile >outfile
```

### 1.5.2 멤버 함수 처음 살펴보기

```cpp
#include <iostream>
#include "Sales_item"

int main() {
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    if (item1.isbn() == item2.isbn()) {
        std::cout << item1 + item2 << std::endl;
        return 0;
    } else {
        std::cerr << "Data must refer  to same ISBM" << std::endl;
        return -1;
    }
}
```

- `item1.isbn()` - 이 부분은 이름이 `isbn`인 멤버 함수를 호출한다. 멤버 함수는 클래스에 정의한 함수이며 **메서드**라고도 한다.
  - 점 연산자를 통해 왼쪽이 클래스, 오른쪽이 클래스의 메서드인 경우 작동하고 호출연산자(())를 통해 인자를 넣거나 안 넣고 호출한다.

## 1.6 시점 프로그램

```cpp
#include <iostream>
#include "Sales_item"

int main() {
    Sales_item total;
    if (std::con >> total) {
        Sales_item trans;
        while (std::cin >> trans) {
            if (total.isbn() == trans.isbn())
                total += trans;
            else {
                std::cout << total << std::endl;
                total = trans;
            }
        }
        std::cout << total << std::endl;

    } else {
        std::cerr << "No data?" << std::endl;
        return -1;
    }
    return 0;
}
```
