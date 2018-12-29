---
title: git blog 관리하기
date: 2018-11-26 19:50:56
tags:
- Git
- Blog
categories:
- Git
---

- 새 저장소(repository) 만들기
  Github에서 새 저장소(repository)를 만든다. 이 때 저장소의 이름을 자신의 username뒤에 `.github.io`가 붙은 이름으로 만든다. 이렇게 만들어 줘야 `username.github.io`의 도메인으로 접속할 수 있는 블로그가 된다.

## **Hexo 설치하기**

git과 node.js는 설치돼 있어야 한다.

```bash
sudo apt install npm
npm install -g hexo-cli # 오류 날 시 앞에 sudo를 붙여준다
```

```bash
hexo -v
```

위의 명령어로 hexo가 제대로 설치 되었는지 확인 한다.

![](/images/1543077067324.png)

Hexo 설치가 완료되었으면 다음과 같은 명령어를 입력해서 Hexo 디렉토리를 초기화한다.

```bash
hexo init <디렉토리명>
```

설치가 모두 잘 되었다면 다음 명령어를 입력해서 내장 서버를 돌릴 수 있다.

```bash
hexo server
```

![](/images/1543077397697.png)

브라우저에서 http://0.0.0.0:4000/ 으로 접속해서 확인 할 수 있다.



## **deploy**

Hexo가 설치된 디렉토리로 가서 _config.yml 파일을 열어

Site, URL, Deployment 항목을 수정해준다.

![](/images/1543079100792.png)

![](/images/1543079046837.png)

그리고 정적 파일을 생성한다.

```bash
hexo generate
```

디플로이를 하기 위해서는 hexo-deployer-git 플러그인이 필요하다. 아래의 명령어를 사용해서 설치한다.

```bash
npm install --save hexo-deployer-git
```

생성이 잘 되었다면 디플로이 명령어를 사용한다.

```bash
hexo deploy
```



## Hueman 테마 적용하기

블로그 루트 폴더에서 명령어로 테마를 받는다.

```bash
git clone https://github.com/ppoffice/hexo-theme-hueman.git themes/hueman
```

blog 폴더에 있는 _config.yml에서 Theme부분을 landscape에서 hueman으로 바꿔준다.

![](/images/1543079535420.png)

themes/hueman 폴더에 있는 `_config.yml.example`을 `_config.yml`로 바꾼다.

```bash
cd blog/themes/hueman
mv _config.yml.example _config.yml
```

최신 버전을 다운받기 위해 pull해준다.

```bash
cd themes/hueman
git pull
```

Hueman 테마의 `Insight Search` 검색엔진을 사용하기 위해 npm으로 `hexo-generator-json-content`을 설치한다.

```bash
npm install -S hexo-generator-json-content
```

hueman의 테마는 hueman폴더 안에 있는 _config.yml에서 설정할 수 있다.



## 포스트 작성하기



```bash
hexo new post [post name]
```

그러면 `[blogFolder]/source/_posts`에 새로운 마크다운 파일이 생성된다.
자동으로 제목과 생성날짜가 들어간다.

글을 마크다운 파일로 작성 한 후

```bash
hexo generate
hexo deploy
```

or

```bash
hexo generate --deploy
```



## 테마가 적용 안되는 경우

```bash
hexo clean
hexo generate --deploy
```

