---
title: Zip 압축 풀 때 한글 파일명 오류 해결법
date: 2019-09-18 20:43:12
tags: Ubuntu
categories: Ubuntu
---

Windows 에서 압축(zip)한 파일을 Linux에서 압축풀때, 한글로 되어 있는 파일이 깨져서 나올 때가 있다. 이는 Windows의 한글 문자셋(CP949)과 Linux의 한글 문자셋(UTF-8)이 다르기에 발생하는 문제이다.



압축해제 명령

```bash
unzip filename.zip
```



인코딩 지정

```bash
unzip -O cp949 filename.zip
```



기본 환경설정에 추가

```bash
vi ~/.profile

export UNZIP="-O cp949"
export ZIPINFO="-O cp949"
```

