# 우분투 root 비밀번호 설정

우분투를 설치하면 기본으로 Root 비밀번호가 없는 상태이다.

아래와 같은 방법으로 root 비밀번호를 설정해본다.



1. root 비밀번호 설정

   ```bash
   sudo passwd
   ```

   ![1543073527838](/home/p829911/.config/Typora/typora-user-images/1543073527838.png)


   위와 같이 비밀번호를 설정 했다면

   ```bash
   su
   ```

   명령을 통해 root에 로그인 할 수 있다.


2. passwd

   ```bash
   passwd
   ```

   현재 로그인한 사용자 계정의 비밀번호를 변경할 수 있는 명령어이다.



3. root에서 user 비밀번호 변경

   ```bash
   passwd p829911
   ```

   root에서 p829911이라는 사용자의 비밀번호를 변경하고 싶을 때 사용하는 명렁어이다.