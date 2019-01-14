# pyenv, virtualenv, autoenv 

###   pyenv

- 파이썬 버전을 관리하는 툴
- 하나의 컴퓨터에 다양한 파이썬 버전을 설치하고 관리



### pyenv-virtualenv

- virtualenv은 파이썬 환경을 격리하는 툴
- pyenv-virtualenv은 virtualenv의 pyenv 확장 플러그인
- 파이썬 버전과 라이브러리의 완전한 격리 환경을 제공



### autoenv

- autoenv는 디렉터리 이동 시 실행되는 스크립트
- pyenv-virtualenv 사용 시 불편한 수작업을 자동화
- 특정 프로젝트 폴더로 들어가면 .env 파일을 실행하여 가상환경 활성화



### 맥, OS X 사전 준비사항

```bash
sudo xcode-select --install
brew install homebrew/dupes/zlib
```



### pyenv 설치

```bash
brew install pyenv

# pyenv 업그레이드
brew upgrade pyenv
```



### 환경변수 적용 및 업데이트

다음 명령을 터미널에서 수행하여 환경변수를 등록한다. zsh를 사용할 때는 `"~/.bash_profile"`을 `"~/.zshrc"`로 변경하여 실행한다.

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
```



### pyenv를 이용한 python 설치

```bash
pyenv install 3.6.5

pyenv versions
* system (set by /Users/p829911/.pyenv/version)
  3.6.5
  3.6.5/envs/tensorflow
  3.7.2
  3.7.2/envs/speech
  speech
  tensorflow
```

여기서 설치가 되지 않고 오류가 나는 경우 다음 명령으로 실행시켜 준다.

```bash
CFLAGS="-I$(brew --prefix openssl)/include -I$(xcrun --show-sdk-path)/usr/include" \
LDFLAGS="-L$(brew --prefix openssl)/lib" \
pyenv install -v 3.6.5
```



### pyenv-virtualenv 사용하기

```bash
# pyenv-virtualenv 설치
brew install pyenv-virtualenv

# 환경변수 설정
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

# virtualenv 생성
pyenv virtualenv <virtualenv-name>

# virtualenv 활성화
pyenv activate <virtualenv-name>

# virtualenv 비활성화
pyenv deactivate

# virtualenv 삭제
pyenv uninstall <version> / <virtualenv-name>
```



### autoenv

```bash
# 설치
brew install autoenv

# 환경설정
echo "source $(brew --prefix autoenv)/activate.sh" >> ~/.bashrc
source ~/.bashrc
```

가상 환경을 활성화 할 폴더에 .env 파일을 만들어 준다.

```bash
vi <virtualenv-folder>/.env

pyenv activate <virtualenv-name>
```

폴더를 나오면 다시 deactivate를 적용시켜 준다.

```bash
vi ~/.env

pyenv deactivate
# or
pyenv shell system
```



### pip를 이용해 라이브러리 설치

가상환경은 pip를 이용해 설치하는 패키지 또한 분리하여 관리해주기 때문에 원래 설치해 두었던 라이브러리들을 다시 깔아 줄 필요가 있다.

```bash
pip3 freeze > requirements.txt
```

위 명령어는 현재 pip3로  python3 환경에서 깔려있는 라이브러리이름과 버전을 requirement.txt 파일에 저장해 주는 명령어이다.

```bash
jupyter==1.0.0
jupyter-client==5.1.0
jupyter-console==5.2.0
jupyter-core==4.3.0
MarkupSafe==1.0
mistune==0.7.4
nbconvert==5.3.1
nbformat==4.4.0
notebook==5.0.0
pandocfilters==1.4.2
pexpect==4.2.1
pickleshare==0.7.4
prompt-toolkit==1.0.15
...
```



requirements.txt 파일에 적힌 모든 라이브러리를 설치하는 pip 명령은 다음과 같다.

가상환경폴더로 이동 한 후

```bash
pip install -r requirements.txt
```

