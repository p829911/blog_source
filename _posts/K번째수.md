---
title: K번째수
date: 2019-01-15 02:10:10
tags:
- Algorithm
categories:
- Algorithm
mathjax: true
---

### **문제 설명**
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.  

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.



### 제한사항

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.



### 입출력 예

| array           | commands                  | return  |
| --------------- | ------------------------- | ------- |
| [1,5,2,6,3,7,4] | [[2,5,3],[4,4,1],[1,7,3]] | [5,6,3] |



### 입출력 예 설명

[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다

[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.  

[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.



### 나의 풀이

```python
array = [1,5,2,6,3,7,4]
commands = [
    [2,5,3],
    [4,4,1],
    [1,7,3],
]
```

```python
def solution(array, commands):
    answer = []
    for command in commands:
        answer.append(sorted(array[command[0]-1:command[1]])[command[2]-1])
    return answer
```



### 다른 사람의 풀이

```python
def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```



### lambda(람다) 함수
lambda 함수는 익명함수로 메모리를 절약하는 이점이 있다.  
일반적인 함수는 객체를 만들고, 재사용을 위해 함수 이름(메모리)를 할당 한다.  

```python
# lambda 인수1, 인수2, ...: 인수를 이용한 표현식
sum = lambda a, b: a + b
result = sum(3,4)
print(result)

# 7
```

익명함수이기 때문에 한번 쓰이고 다음줄로 넘어가면 힙(heap) 메모리 영역에서 증발하게 된다.  
자세하게 설명하자면 파이썬에서 모든 것이 객체로 관리되고 각 객체는 레퍼런스 카운터를 갖게 되는데 해당 카운터가 0 - 어떤 것도 참조를 하지 않으면 메모리를 환원한다 - 이러한 역할을 하는 것이 가비지 컬럭터이다.



### map 함수
내장함수이며 입력받은 자료형의 각 요소가 함수에 의해 수행된 결과를 묶어서 map iterator 객체로 반환한다. map 함수는 게으른 연산을 진행해서 메모리를 크게 절약할 수 있다. 게으른 연산을 진행하기 때문에 값을 한번 사용했던 값은 다시 호출할 수가 없다.

```python
# map(function, iterable)
# 예시
li = [1,2,3]
result = list(map(lambda i: i ** 2, li))
print(result)

# [1,4,9]
```



### 게으른 연산이란(lazy evaluation)?
필요할 때만 가져다 사용한다. 보통 iterator 객체들이 게으른 함수이다.
> iterator 객체

- next() 메소드로 데이터를 순차적으로 호출 가능
- 마지막 데이터 이후 next()를 호출하면 StopIteration 에러 발생
- for 문을 사용할 때, 파이썬 내부에서는 임시로 list를 iterator로 변환해서 사용