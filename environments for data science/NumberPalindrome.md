---
title: NumberPalindrome
date: 2019-01-21 15:55:37
tags:
- Algorithm
categories:
- Algorithm
mathjax: true
---

0 에서 `10**n-1` 사이의 정수 `10**n` 개 중에서, 
그냥 보았을때, 그리고 역순으로 뒤집어서 보았을때 같은 숫자를 카운트 하는 함수를 작성하세요.

**조건**

`def solution(n):`

n은 1부터 1000까지 정수중 하나

**예**

n = 1 인 경우 0부터 `10**`까지 즉 10까지 숫자중 회문이 성립하는 순자의 갯수를 카운트

`1, 2, 3, 4, 5, 6, 7, 8, 9` 이 성립 

10을 리턴

----

뒤집어도 같은 정수란 3, 44, 12321 과 같은 정수들을 뜻합니다.



### 내가 푼 코드

```python
def solution(n):
    total = 10
    
    if n == 1:
        return total
    
    for i in range(11, 10**n):
        ls = list(str(i))
        l = len(ls)
        if l % 2 == 1:
            a = int((l-1)/2)
        else:
            a = int(l/2)
      
        if ls[:a] == ls[-a:]:
            total += 1
            
    return total
```



### 단순한 코드

```python
def solution(n):
    count = 0
    for number in range(0, (10**n)+1):
        str_number = str(number)
        if str_number == str_number[::-1]:
            count += 1
    return count
```



### 효율적인 코드

점화식으로 만든 후 재귀 함수 사용

```
1자리수일때: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 -> 10개
2자리수일때: 11, 22, 33, 44 ,55 ,66 ,77 ,88, 99 -> 9개
3자리수일때: 1x1, 2x2, 3x3, ....,9x9 -> 9 * 10개
4자리수일때: 1xx1, 2xx2,......, 9xx9 -> 9 * 10개
5자리수일때: 1xyx1, ....... , 9xyx9 -> 9 * 10 * 10개
```



```python
def solution(n):
    if n == 1:
        return 10
    return solution(n-1) + 9 * (10 ** ((n-1)//2))
```



### 점화식

$$
A1 = a \\
A2 = a + d \\
An = A(n-1) + d
$$

a가 3 d가 2일 때 재귀함수

```python
def a(n):
    if n == 1:
        return 3
    return a(n-1) + 2
```



### 피보나치 수열

```python
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```



### memorization

```python
def make_memo(func):
    me = {}
    def memo(n):
        if me.get(n):
            return me[n]
        else:
            result = func(n)
            me[n] = result
            return result
    return memo
```

```python
@make_memo
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```



### functors 패키지의 leu_cache

```python
@lru_cache(maxsize=128)
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```



#### decoration 추가 공부 하기

#### 풀기 전에 5분 ~ 10분 정도 충분히 생각한 후 가장 효율적인 방법이라고 생각하는 코드를 짠다. 코드 짜기 부터 하지 말자.