---
layout: page
title: 分类
permalink: /categories/
---

{% for category in site.categories %}
### {{ category[0] }}
{% for post in category[1] %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}
{% endfor %}
