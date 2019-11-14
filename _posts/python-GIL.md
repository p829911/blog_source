---
title: python GIL
date: 2019-11-11 14:12:22
tags:
- Python
- GIL
categories:
- Python
---

### Python GIL

##### Global Interpreter Lock

> In CPython, the global interpreter lock, or GIL, is a mutex that protects access to python objects, preventing multiple threads from executing Python bytecodes at once. This lock is necessary mainly because CPython's memory management is not thread-safe.



##### Process & Thread

![](https://user-images.githubusercontent.com/17154958/68179529-99801080-ffd3-11e9-9da8-a41e31077e66.png)

운영체제가 생성하는 작업 단위를 process라고 한다. 이 process 안에서 공유되는 메모리를 바탕으로 여러 작업을 또 생성할 수 있는데, 이 때의 작업 단위를 thread라고 한다 따라서 각 thread 마다 할당된 개인적인 메모리가 있으면서, thread가 속한 process가 가지는 메모리에도 접근할 수 있다.

`Thread-safe` 하지 않다는 것은 무슨 의미인지 부터 알아보겠다. 위에서 thread들은 process가 공유하는 메모리에 접근할 수 있다고 언급했는데, 이로 인해 참사가 발생할 수 있다.

```python
import threading

x = 0 # A shared value

def foo():
    global x
    for i in range(1000000):
        x += 1
        
def bar():
    global x
    for i in range(1000000):
        x -= 1
        
t1 = threading.Thread(target=foo)
t2 = threading.Thread(target=bar)
t1.start()
t2.start()
t1.join()
t2.join() # Wait for completion

print(x)
```

`print(x)` 의 결과가 0으로 나오는게 정상적으로 작동한 것이다. 하지만 실제 계산을 해보면 `x`의 값은 전혀 이상한 숫자가 된다. 전역 변수 `x`에 두 개의 thread가 동시에 접근해서 각자의 작업을 하면서 어느 한 쪽의 작업 결과가 반영이 되지 않기 때문이다. 이렇게 여러 thread가 공유된 데이터를 변경함으로써 발생하는 문제를 `race condition` 이라고도 부른다.

따라서 `thread-safe` 하다는 것은 thread들이 `race condition`을 발생시키지 않으면서 각자의 일을 수행한다는 뜻임을 알 수 있다.



##### mutex

`Thread-safe`한 코드를 만들기 위해서 사용하는 것 중 하나가 mutex (mutual exclusion)이다. `race condition`을 막기 위해서, 공유되는 메모리의 데이터를 여러 thread가 동시에 사용할 수 없도록 잠그는 일을 mutex가 맡는다.

>휴대폰이 없던 시절에는 공중 전화를 주로 이용했었다. 거리의 모든 남자들은 각자의 아내에게 전화를 너무나 걸고 싶어한다.
>
>어떤 한 남자가 처음으로 공중 전화 부스에 들어가서 그의 사랑하는 아내에게 전화를 걸었다면, 그는 꼭 전화 부스의 문을 꼭 잡고 있어야 한다. 왜냐하면 사랑에 눈이 먼 다른 남자들이 전화를 걸기 위해 시도때도 없이 달려들고 있기 때문이다. 줄 서는 질서 문화 따위는 없다. 심지어 그 문을 놓친다면, 전화 부스에 들이닥친 남자들이 수화기를 뺏어 당신의 아내에게 애정 표현을 할 지도 모른다.
>
>아내와의 즐거운 통화를 무사히 마쳤다면, 이제 문을 잡고 있던 손을 놓고 부스 밖으로 나가면 된다. 그러면 공중 전화를 쓰기 위해 달려드는 다른 남자들 중 제일 빠른 한 명이 부스에 들어가서 똑같이 문을 꼭 잡고 그의 아내와 통화할 수 있다.

- thread: 각 남자들
- mutex: 공중 전화 부스의 문
- lock: 그 문을 잡고 있는 남자의 손
- resource: 공중 전화



CPython이 `reference counting`을 하는 과정에서 문제가 일어날 수 있음을 알 수 있다.
Reference counting 중에 `race condition`이 일어난다면, 그 결과는 결국 메모리 유실(memory leak)일 것이다. (반대로 살아있어야 할 Object를 죽여버릴 수도 있다.) 
이를 해결하기 위해서는 mutex를 이용하면 된다고 했다.
CPython의 결정은 mutex를 통해 모든 reference 개수를 일일이 보호하지 말고, Python interpreter 자체를 잠그기로 한 것이다. 이거 하나만 mutex로 보호하면 그동안 우려했던 문제를 해결할 수 있다. 하지만, 얼마나 많은 thread를 사용하던지에 상관없이 오직 한 thread만이 Python code를 실행할 수 있다는 의미이기도 하다.



##### 왜 GIL을 선택했나?

Python이 태동하던 시기에는 thread라는 개념이 없었을 당시였고, 쉽고 간결한 언어를 표방했던 Python에 많은 사용자들이 모여들고 있었다. 수 많은 C extension들이 이미 만들어졌는데, 시간이 지나서 thread 개념으로 인한 문제를 해결하기 위해서 가장 현실적인 방안은 GIL이었다. 거대한 커뮤니티에서 만들어낸 C extension들을 새로운 메모리 관리 방법에 맞춰서 모두 바꾸는 것은 불가능하다. 대신 Python이 GIL을 도입하면 C extension들을 바꾸지 않아도 됐던 것이다.



##### 결론

- 병렬 처리에 관해서는 굳이 thread가 아니더라도 multiprocessing이나 asyncio 등의 많은 선택지가 있다.



##### 출처

- https://dgkim5360.tistory.com/entry/understanding-the-global-interpreter-lock-of-cpython
- https://magi82.github.io/process-thread/
- https://118k.tistory.com/606
- H3 2011 파이썬으로 클라우드 하고 싶어요_분산기술Lab 하용호 From KTH, 케이티하이텔

<p><iframe src="//www.slideshare.net/slideshow/embed_code/key/5CUCEe3yKs2LyP?startSlide=56" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border: 1px solid rgb(204, 204, 204); margin-bottom: 5px; max-width: 100%; width: 820px; height: 668.403px;" allowfullscreen=""> </iframe> </p>

- [2D4]Python에서의 동시성_병렬성 from NAVER D2

<p><iframe src="//www.slideshare.net/slideshow/embed_code/key/hNgCkfPVcKCUbL?startSlide=15" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border: 1px solid rgb(204, 204, 204); margin-bottom: 5px; max-width: 100%; width: 820px; height: 668.403px;" allowfullscreen=""> </iframe> </p>