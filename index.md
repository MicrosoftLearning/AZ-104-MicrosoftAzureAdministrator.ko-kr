---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
---

# 콘텐츠 디렉터리

필수 랩 파일은 여기에서 다운로드할 [수 있습니다.](https://github.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator/archive/master.zip)

## 랩

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 모듈 | 랩 |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}

## 데모

{% assign demos = site.pages | where_exp:"page", "page.url contains '/Instructions/Demos'" %}
| 모듈 | 데모 |
| --- | --- | 
{% for activity in demos  %}| {{ activity.demo.module }} | [{{ activity.demo.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
