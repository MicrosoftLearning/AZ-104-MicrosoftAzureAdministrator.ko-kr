---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
---

# 콘텐츠 디렉터리

필요한 랩 파일은 [여기에서 다운로드](https://github.com/MicrosoftLearning/AZ-104KO-MicrosoftAzureAdministrator/archive/master.zip)할 수 있습니다.

아래에는 각 랩 연습의 하이퍼링크 목록이 나와 있습니다.

## 랩

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 모듈 | 랩 |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}


