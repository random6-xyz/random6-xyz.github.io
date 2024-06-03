---
layout: post
title: "[baekjoon] 2581 python"
category: [coding test, baekjoon]
date: 2024-06-03 13:33:40 +0900
tag: [algorithm, PS, python]
description: algorithm
comments: false
---

## Problem

The problem is to find minimum and sum of prime numbers in the range `M` to `N`.

## First try

```python
M = int(input())
N = int(input())

def prime_calc(num):
    list = [True] * num

    for i in range(2, int(num**0.5)+1):
        if list[i] == True:
            for j in range(i*2, num, i):
                list[j] = False
    return [i for i in range(2, num) if list[i] == True]

m_prime = prime_calc(M)
n_prime = prime_calc(N+1)
list_prime = list(set(n_prime) - set(m_prime))
if not list_prime:
    print(-1)
else: 
    print(sum(list_prime))
    print(list_prime[-1])
```

- `prime_calc` function returns prime list from 2 to `num`
  - Finding prime numbers was implemented through **Eratosthenes' sieve.**
  - Actually **Sieve of Atkin** is the fastest algorithm to find prime numbers. but It is pretty hard to implement with python. So, I use Eratosthenes' sieve.
- find two lists
  - prime numbers from 2 to M-1
  - prime numbers from 2 to N
- sub two lists
  - (2 to N) - (2 to M-1)
- print result

## Result of first try

- Sample case was all passed but the final test was failed. So, I searched for another samples on the question board.
- `1 4 → 5 3` → When I was typing something not important, I found my counterexample
  - The reason I was wrong is that I thought the list was sorted. But it wasn't. So, I modified my last line.

## Final try

```python
M = int(input())
N = int(input())

def prime_calc(num):
    list = [True] * num

    for i in range(2, int(num**0.5)+1):
        if list[i] == True:
            for j in range(i*2, num, i):
                list[j] = False
    return [i for i in range(2, num) if list[i] == True]

m_prime = prime_calc(M)
n_prime = prime_calc(N+1)
list_prime = list(set(n_prime) - set(m_prime))
if not list_prime:
    print(-1)
else: 
    print(sum(list_prime))
    print(min(list_prime))
```

## Result of final try

- final test was passed.

## Conclusion

- Do not assume that lists are sorted.
