---
title: crontab
date: 2019-01-11 11:53:56
tags:
- Ubuntu
- Crontab
categories:
- Ubuntu
mathjax: true
---

[리눅스 크론탭 사용법](https://jdm.kr/blog/2)

> "특정 시간에 특정 작업을 해야한다."



#### 1. 크론탭 기본 (crontab basic)

```bash
# 크론탭 실행
crontab -e

# 현재 크론탭에 어떤 내용이 들어있는지 보기
crontab -l

# 크론탭을 지우고 싶을 때
crontab -r

# 저장은 vi 처럼 콜론(:) 입력 후 wq로 갱신
***** ls -al

# 별이 다섯개 있는 경우에 "매분마다 실행"
```

#### 2. 주기 결정

```bash
*			*			*			*			*
분(0-59)	   시간(0-23)   일(1-31)	  월(1-12)	  요일(0-7)
```

각 별 위치에 따라 주기를 다르게 설정 할 수 있다. 순서대로 **분-시간-일-월-요일** 순이다. 그리고 괄호 안의 숫자 범위 내로 별 대신 입력할 수 있다.

요일에서 0과 7은 일요일이다. 1부터 월요일이고, 6이 토요일이다.

#### 3. 주기별 예제

```bash
# 매분 test.sh 실행
* * * * * /home/script/test.sh

# 매주 금요일 오전 5시 45분에 test.sh 를 실행
45 5 * * 5 /home/script/test.sh

# 매일 매시간 0분, 20분, 40분에 test.sh 를 실행
0,20,40 * * * * /home/script/test.sh

# 매일 1시 0분부터 30분까지 매분 test.sh 를 실행
0-30 1 * * * /home/script/test.sh

# 매 10분마다 test.sh 를 실행
*/10 * * * * /home/script/test.sh

# 5일에서 6일까지 2시, 3시, 4시에 매 10분마다 test.sh를 실행
*/10 2,3,4 5-6 * * /home/script/test.sh
```

> 주기 입력 방법엔 *, - , / 을 이용하는 방법이 있다. 위에서 봤듯이 각각의 특수기호가 하는 기능이 다르고 조합을 어떻게 하느냐에 따라 주기를 설정 할 수 있다.

#### 크론 사용 팁

```bash
# 한 줄에 하나의 명령만 쓴다. 
# 잘못된 예
* * * 5 5
/home/script/test.sh

# 잘된 예
* * * 5 5 /home/script.test.sh
```

#### 크론 로깅 (cron logging)

해당 처리 내역에 대해 로그를 남기고 싶을 때

```bash
* * * * * /home/script/test.sh > /home/script/test.sh.log 2>&1
```

위에서 2>&1이란
make를 하면 일반 출력은 stdout, 에러 메시지는 stderr로 출력 된다.
stderr을 stdout으로 돌려서 에러 메세지도 저장되게 하라는 의미이다.
n>&m: 표준 출력과 표준 에러를 서로 바꾸기

- 0: 표준 입력
- 1: 표준 출력
- 2: 표준 에러

너무 자주 실행 되고 지속적으로 로깅이 되야 해서 로그를 계속 남겨둬야 한다면

```bash
* * * * * /home/script/test.sh >> /home/script/test.sh.log 2>&1
```

위의 코드를 실행하면 계속 로그가 누적이 되는 것을 확인 할 수 있다. 그러나 로그가 과도하게 쌓이면 리눅스 퍼포먼스에 영향을 주므로 가끔씩 비워주거나 파일을 새로 만들어주는 작업이 필요하다.

#### 크론탭 백업 (crontab backup)

혹시라도 `crontab -r`을 쓰거나 실수로 crontab 디렉토리를 날려버려서 기존 크론 내역들이 날아갔을 때를 대비하여 주기적으로 크론탭을 백업해 주어야 한다.

```bash
crontab -l > /home/bak/crantab_bak.txt
```

크론탭 내용을 txt파일로 만들어 저장해 두는 것이다.

```bash
# 자동화
50 23 * * * crontab -l > /home/bak/crontab_bak.txt
```

매일 오후 11시 50분에 크론탭을 백업해 두는 명령어이다.



