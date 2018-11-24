# ubuntu 한글 입력기 설치

## 한글 설치

1. fcitx-hangul 설치

```bash
sudo apt-get install fcitx-hangul
```

2. System Setting (설정) > Language Support(언어 지원) 을 실행해서 설치되지 않은 언어팩 모두 설치한다.
3. 키보드 입력기를 ibus에서 fcitx로 변경한다.
4. 재부팅 시 오른쪽 위에 아래의 첫번째에서 보는 것과 같은 아이콘이 생성된 것을 볼 수 있다.

![1543073119942](/images/1543073119942.png)

## 한영 변환

1. 설정 > 장치 > 키보드 로 들어간 뒤 입력 중의 다음 입력소스로 전환, 이전 입력소스로 전환을 사용 않음으로 바꿔준다. 사용 않음으로 바꿔주기 위해선 클릭 후 backspace를 누르면 된다.
2. 상단 메뉴바 오른쪽의 입력기 선택(위 그림에서 세번째) 후 현재 입력기 설정 클릭
3. Keyboard-English(US)가 있다면 + 를 눌러 Hangul을 추가한다. (uncheck "Only Show Current Language"). Korean이 아닌 Hangul을 선택한다.
4. 전역 설정 > 단축키 > 입력기 전환에 'Shift + Space'를 추가한다.
5. 전역 설정 > 프로그램 윈도우 사이에 상태 공유를 '모두'로 바꿔준다