---
title: Jupyber notebook matplotlib 한글 설정
date: 2018-11-26 22:25:40
tags: Jupyter, Python
categories:
- Python
---

우분투 폰트 경로 /usr/share/fonts/

나눔 글꼴 또는 다른 폰트도 /usr/share/fonts/ 폴더에 복사에서 사용가능하다.



**나눔글꼴 설치**

```bash
sudo apt-get install fonts-nanum*
sudo fc-cache -fv
```

apt-get 명령으로 나눔글꼴 설치 후, fc-cache 명령으로 폰트 캐시 삭제



**다른 ttf 폰트**

```bash
sudo cp new_font.ttf / usr/share/fonts
sudo fc-cache -fv
```

우분투 폰트 경로로 ttf폰트 복사 후, fc-cache 명령으로 폰트 캐시 삭제



**matplotlib 폴더에 글꼴  추가**

```bash
sudo cp /usr/share/fonts/truetype/D2Coding/D2* /home/p829911/.local/lib/python3.6/site-packages/matplotlib/mpl-data/

rm -rf /home/ubuntu/.cache/matplotlib/*
```

matplotlib 폴더에 글꼴을 복사 한 후 matplotlib의 폰트 캐시를 삭제

```python
# 캐쉬 디렉토리
matplotlib.get_cachedir()
```



**내 컴퓨터에 저장되어 있는 폰트 리스트 가져오기**

```python
import matplotlib.font_manager as fm

font_list = fm.findSystemFonts(fontpaths=None, fontext='ttf')

# 전체개수
print(len(font_list)) 

# 처음 10개만 출력
font_list[:10] 
```



**사용가능한 시스템의 TTF 폰트 목록**

```python
import matplotlib.font_manager as fm

font_list = [(f.name, f.fname) for f in fm.fontManager.ttflist]
print(len(font_list))

font_list[:10]
```



**내가 원하는 D2Coding 폰트의 저장 위치를 불러오기**

```python
for font in font_list:
    if "D2" in font[0]:
        print(font)
```



**rcParams 를 설정 파일에 직접 적어주기 - 모든 노트북에 공통 적용**

- font.family: D2Coding
- 이곳에 폰트를 지정해 주면 노트북을 실행 할 때 바로 로드되도록 설정할 수 있다.

```python
print(matplotlib.matplotlib_fname())
```

```bash
vi /home/p829911/.local/lib/python3.6/site-packages/matplotlib/mpl-data/matplotlibrc
```

matplotlibrc파일에서 font.family를 D2Coding으로 설정해준다.



![](/images/1543238354268.png)



```python
import numpy as np
import matplotlib.pyplot as plt

%matplotlib inline

data = np.random.randint(-100, 100, 50).cumsum()
data
plt.plot(range(50), data, 'r')
plt.title('가격변동 추이')
plt.ylabel('가격')
plt.show()
```

![](/images/1543238573921.png)

