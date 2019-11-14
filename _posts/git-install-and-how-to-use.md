---
title: git 설치 & 사용법
date: 2018-12-03 21:58:52
tags:
- Git
- Ubuntu
categories:
- Git
---



### git은 터미널에서 다음과 같은 명렁어로 설치 할 수 있다.

```bash
sudo apt-get install git
```

설치가 완료 되었으면

```bash
git --version
```

git config 설정

```bash
git config --global user.name "username"
git config --global user.email "github email address"
git config --global core.editor "vim"
git config --list
```



### local에 있는 폴더와 git 저장소 연동시키기

- 폴더 생성 후 git init 해주기

```bash
git init
git add.
git commit -m "contents"
```

- git repository 생성 해 준 후

```bash
git remote add origin https://github.com/username/repo.git
git push origin master
```

- 위의 코드에서 origin이라는 부분은 사용자가 지정할 수 있지만, 보통 origin이라고 써줌
- git 에서 저장소를 clone 할 때는 자동적으로 origin이라고 지정 된다.



### git 저장소 local 폴더로 복제하기

```bash
git clone https://github.com/username/repo.git
```

개인적으로는 git remote 보다 git clone해서 사용하는 것이 더 편하다.



### branch

소프트웨어를 개발할 때 개발자들은 동일한 소스코드를 함께 공유한다. 동일한 소스코드 위에서 서로 다른 작업을 할 때는 각각 서로 다른 버전의 코드가 만들어 질 수 밖에 없다.
이럴 때, 여러 개발자들이 동시에 다양한 작업을 할 수 있게 만들어 주는 기능이 바로 '브랜치(Branch)'이다.
이렇게 분리된 작업 영역에서 변경된 내용은 나중에 원래의 버전과 비교해서 하나의 새로운 버전으로 만들어 낼 수 있다. 

브랜치란 독립적으로 어떤 작업을 진행하기 위한 개념이다. 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있다.

또한 이렇게 만들어진 브랜치는 다른 브랜치와 병합(Merge)함으로써, 작업한 내용을 다시 새로운 하나의 브랜치로 모을 수 있다.

저장소를 처음 만들면, Git은 바로 'master'라는 이름의 브랜치를 만들어 준다. 이 새로운 저장소에 새로운 파일을 추가한다거나 추가한 파일의 내용을 변경하여 그 내용을 저장(커밋, commit)하는 것은 모두 'master'라는 이름의 브랜치를 통해 처리할 수 있다.

```bash
git branch <branchname> # 브랜치 생성
git branch # 브랜치 확인
git branch -r # remote 브랜치 확인
git branch -a # 모든 사용가능한 브랜치 확인
git checkout <branchname> # 브랜치 지정
git checkout -b <branchname> # 브랜치 생성, 체크아웃
git merge <branchname> # 브랜치 병합
git branch -d <branchname> # 브랜치 삭제
```



**참고**

- https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html
- https://github.com/ulgoon/dss-linux-git

