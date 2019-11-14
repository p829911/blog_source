---
title: python gc collect
date: 2019-11-11 14:13:05
tags:
- GC Collect
- Python
categories:
- Python
---

### python gc collect

보통 파이썬은 레퍼런스 카운팅 방식으로 가비지 컬렉션을 수행해 메모리를 관리하고, 레퍼런스 카운팅을 사용했을 때 발생할 수 있는 순환 참조 상황을 별도의 가비지 컬렉터로 해결한다고 알고 있다.

python에는 Garbage Collection이라는 것이 있기 때문에 C/C++ 처럼 메모리를 직접 할당/해제하는 수고를 하지 않아도 되며 메모리를 직접 다룸으로 인해 발생되는 수많은 버그나 위험으로 부터 안전한 편이다. 왜냐하면 Garbage Collection이라는 것이 생성된 객체들을 순회하며 해당 객체가 현재 쓰이는 곳이 없을 경우 자동으로 해제를 해주기 때문이다. 그렇다고 사용자가 아무것도 하지 않아서는 안된다. Garbage Collection이 쓸모 없어진 객체들을 잘 해제할 수 있도록 레퍼런스 카운트에 신경을 써주어야 한다. 특히, 순환참조의 경우는 프로그램이 종료될때까지 메모리에 남아 있게 되므로 특히 주의 하여야한다.

#### GC는 어떨 때 사용할까?

파이썬에선 기본적으로 garbage collection과 reference counting을 통해 할당된 메모리를 관리한다.
기본적으로 참조 횟수가 0이 된 객체를 메모리에서 해제하는 레퍼런스 카운팅 방식을 사용하지만, 참조 횟수가 0은 아니지만 도달할 수 없는 상태인 reference cycles(순환 참조) 가 발생했을 때는 가비지 컬렉션으로 그 상황을 해결한다.

> 엄밀히 말하면 레퍼런스 카운팅 방식을 통해 객체를 메모리에서 해제하는 행위가 가비지 컬렉션의 한 형태지만 여기서는 순환 참조가 발생했을 때 cyclic garbage collector를 통한 **가비지 컬렉션**과 **레퍼런스 카운팅**을 통한 가비지 컬렉션을 구분했다.

#### 레퍼런스 카운팅

모든 객체는 참조 당할 때 레퍼런스 카운터를 증가시키고 참조가 없어질 때 카운터를 감소시킨다.
이 카운터가 0이 되면 객체가 메모리에서 해제 된다. 어떤 객체의 레퍼런스 카운트를 보고 싶다면 `sys.getrefcount()` 로 확인할 수 있다.

#### 순환 참조의 예

```python
l = []
l.append(l)
del l
```

`l`의 참조 횟수는 1이지만 이 객체는 더 이상 접근할 수 없으며 레퍼런스 카운팅 방식으로는 메모리에서 해제될 수 없다.

```python
class A:
    def __del__(self):
        print("Deleted")
        
a = A()
del(a)

# 결과: Deleted
```



```python
class A:
    def __del__(self):
        print("Deleted")
        
a = A()
b = a

del(a)
# 결과: None
```

이전과는 다르게 delete라는 메시지를 출력하지 않는다. 즉, a라는 객체가 메모리에서 지워지지 않았다는 얘기이다. 왜냐하면 b라는 변수에서 a를 참조중이기 때문이다. 

##### 오브젝트가 현재 참조중인 목록 알아내기

`gc.get_referents`

##### 오브젝트를 참조중인 목록 알아내기

`gc.get_referrers(a)`



- 출처
  - https://weicomes.tistory.com/277
  - https://wikidocs.net/13969
  - https://winterj.me/python-gc/