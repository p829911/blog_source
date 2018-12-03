---
title: ubuntu apt 명령어
date: 2018-11-27 16:50:51
tags:
- Ubuntu
categories:
- Ubuntu
---

우분투에서 패키지를 관리하는 명령어가 몇 가지 있다.

그 중 apt-get과 apt-cache를 결합한 apt에 관한 명령어를 알아보겠다.



1. **패키지 목록 갱신**

   ```bash
   apt update
   ```


2. **모든 패키지를 최신 버전으로 업그레이드**

   ```bash
   apt install upgrade
   apt full-upgrade # 의존성 고려한 패키지 업그레이드
   ```



3. **패키지 설치**

   ```bash
   apt install package_name
   ```



4. **패키지 삭제**

   ```bash
   apt remove package_name
   ```



5. **패키지 삭제(설정 파일 포함)**

   ```bash
   apt purge package_name
   ```



6. **불필요한 패키지 제거**

   ```bash
   apt autoremove
   ```


7. **패키지 검색**

   ```bash
   apt search package_name
   ```



8. **패키지 상세 정보 출력**

   ```bash
   apt show package_name
   ```


8. **apt 명령어 사용법 & 옵션**

   ```bash
   apt -h
   ```


9. **패키지 리스트 출력**

   ```bash
   apt list
   ```


**권한 문제가 발생할 경우 sudo 명령을 붙여 root로 실행할 수 있다.**