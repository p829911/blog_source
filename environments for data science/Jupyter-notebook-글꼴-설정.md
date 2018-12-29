---
title: Jupyter notebook 글꼴 설정
date: 2018-11-26 19:51:23
tags:
- Jupyter
- Python
categories:
- Python
---

[D2Coding 설치](https://github.com/naver/d2codingfont)

![](/images/1543128432857.png)



```bash
cd /home/username/.jupyter
mkdir custom
cd custom
touch custom.css
vi custom.css
```

만약 custom.css에 쓰기 권한이 없으면 chmod명령으로 파일 권한을 바꿔준다.

```bash
sudo chmod 777 custom.css
```



vi 편집기로 custom.css 파일을 연 후 다음과 같이 설정 해 준다.

```css
 .CodeMirror pre {font-family: D2Coding; font-size: 12pt; line-height: 120%;}
```



jupyter notebook을 실행하면 글꼴이 D2Coding으로 바뀐 것을 볼 수 있다.



