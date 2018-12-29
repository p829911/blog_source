---
title: hexo mathjax
date: 2018-11-26 23:36:53
tags:
- Git
- Blog
- Mathjax
categories:
- Git
mathjax: true
---



### rendering engine change 

Hexo의 기본 renderer인 hexo-renderer-marked는 mathjax 문법을 지원하지 않는다.

따라서 mathjax를 지원하는 rendering engine으로 교체해준다.

```bash
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-kramed --save
```



`<blog dir>/node_modules/hexo-renderer-kramed/lib/renderer.js`를  열어 return값을 text로 수정한다.

```javascript
function formatText(text) {
  // Fit kramed's rule: $$ + \1 + $$
  // return text.replace(/`\$(.*?)\$`/g, '$$$$$1$$$$');
  return text;
}
```



### install mathjax 

mathjax plugin 설치

```bash
npm install hexo-renderer-mathjax --save
```

`<blog dir>/node_modules/hexo-renderer-kramed/node_modules/hexo-renderer-mathjax/mathjax.html` 을 열고 URL을 수정해준다.

```html
<!-- <script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script> -->
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_CHTML'></script>
```



### LaTex와 markdown 문법 충돌 해결하기

`<blog dir>/node_modules/kramed/lib/rules/inline.js`를 열고 다음과 같이 수정한다.

```javascript
escape: /^\\([`*\[\]()#$+\-.!_>])/,
em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```



### Mathjax 사용하기

사용하고 있는 theme의 `_config.yml`파일을 열고 다음과 같이 수정한다.

```yaml
mathjax:
	enable: true
```



### markdown post 작성

post 작성시 header 부분에 `mathjax: true`를 넣어주면 블로그에서 수식이 보이게 된다.