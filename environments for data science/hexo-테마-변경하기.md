---
title: hexo 테마 변경하기
date: 2018-12-13 23:05:43
tags:
- Git
- Blog
categories:
- Git
---

## hexo 폰트 변경

| 나눔스퀘어라운드 (NanumSquareRound)                          |
| ------------------------------------------------------------ |
| https://cdn.rawgit.com/innks/NanumSquareRound/master/nanumsquareround.css |

### head.ejs 수정하기

```
<%- css('https://cdn.rawgit.com/innks/NanumSquareRound/master/nanumsquareround.css') %>
```

```bash
vi blog/themes/hueman/layout/common/head.ejs
```

- head 부분에 추가

![image](https://user-images.githubusercontent.com/17154958/49945337-fd1ecc80-ff2f-11e8-892f-29192aff381f.png)

가운데 보면 위의 코드를 넣어 준 것을 볼 수 있다.



### css 적용

```bash
vi blog/themes/hueman/source/css/_variables.styl
```

![image](https://user-images.githubusercontent.com/17154958/49945516-6a326200-ff30-11e8-8a71-0bbd3985fd89.png)

- font-sans 본문 폰트 : NanumSquareRound 추가
- font-mono 코드 폰트 : D2Coding을 추가



## hexo theme color 변경

![image](https://user-images.githubusercontent.com/17154958/49945678-c0070a00-ff30-11e8-881f-4d041926080f.png)

위와 같이 hueman 테마의 색상을 변경할 수 있다.

```bash
vi blog/themes/hueman/source/css/_variables.styl
```

![image](https://user-images.githubusercontent.com/17154958/49945818-078d9600-ff31-11e8-9efe-6499c268cb6f.png)

- color-default: hexo 폴더 안에 있는 _config.yml 파일에서 설정해 줄 수 있는 색상이다.  위에 사진에 보이는 follow 부분에 나타나는 색상을 적용해 줄 수 있다, 여기서 적용하지 말고 _config.yml파일에서 바꿔준다.
- color-header-background: 위에 보이는 파란색 영역에 색상을 지정해 줄 수 있다.
- color-border: 위에 보이는 노란색 영역에 색상을 지정해 줄 수 있다.
- color-nav-background: 검은색 영역에 색상 지정
- color-footer-background: 맨 밑의 영역에 색상 지정 
- color-sidebar- background: sidebar의 배경색은 모바일에서는 바뀌지만, 데스크탑 사이트에서는 바뀌지 않는다 이 부분의 문제점은 좀 더 찾아봐야할 것 같다.



### 아래의 링크에서 색상 선택에 도움을 받을 수 있을 것이다.

### [Hex Color Code](https://www.color-hex.com/)

