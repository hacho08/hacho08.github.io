---
title: Google Analytics 적용하기
author: 조현아
date: 2021-12-15 01:14:00 +0900
categories: [Blogging]
tags: [Google Analytics]
math: true
mermaid: true
---

이번 블로그는 [**Google Analytics**](https://analytics.google.com/analytics/web/#/)를 적용해본 과정에 대해 적어보겠습니다!


## 시작하기

[**Google Analytics**](https://analytics.google.com/analytics/web/#/) 에 들어가서 계정을 만들어 줍니다.


## 측정 ID받아오기

가입 후에 웹사이트 왼쪽 하단에 세팅을 들어갑니다.
세팅 > 관리자 > 속성 > 데이터 스트림 에 들어가서 스트림 추가를 클릭하여 웹사이트의 URL을 넣어줍니다!
넣어주고 나면 측정 ID와 html 코드가 생성됩니다.


## 블로그에 적용하기 

1. `_config.yml` 파일에서 

```yaml
google_analytics:
  id: 'G-V6XXXXXXX'   # fill in your Google Analytics ID
  # Google Analytics pageviews report settings
  pv:
    proxy_endpoint:   # fill in the Google Analytics superProxy endpoint of Google App Engine
    cache_path:       # the local PV cache data, friendly to visitors from GFW region
```
{: file="_config.yml"}

id 부분에 위에서 생성한 'G-XXXXXXXX' 형식으로 생긴 측정 ID를 넣어줍니다. 

2.  `_includes` 폴더에 들어가면 `google-analytics.html` 라는 파일이 있습니다.
이 파일에서는 이미 위에서 생성된 html 코드가 id 부분만 {{ site.google_analytics.id }} 이렇게 바뀌어서 들어있긴 하지만 변경없이 실행했더니 되지 않아서 다시 복붙을 해줬습니다.
google analytics 웹사이트에서 복사해둔 html코드를 해당 파일에 붙여넣습니다.  
복붙을 해오면 아이디가 들어가 있는데 나중에 혹시 모를 상황을 위해 id를 넣어주는 부분에만 {{ site.google_analytics.id }} 이렇게 변경해주었습니다.


```google-analytics.html
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id= ID 넣어준는 부분 "></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', ' ID 넣어준는 부분 ');
</script>
```
{: file="google-analytics.html"}


## 적용된 것 확인하기 

1. 블로그에 들어가서 새로고침을 해줍니다.
2. Google Analytics 사이트 왼쪽 네비게이션 바에서 
보고서 > 실시간 에 들어가면 사용자 수가 변경되어있다면 성공입니다!!

