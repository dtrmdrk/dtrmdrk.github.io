---
layout: default
title: 图像
permalink: /image/
---
<ul class="post-list">
{% for post in site.categories.图像 %}
<li>
  <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  <a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}
</ul>
