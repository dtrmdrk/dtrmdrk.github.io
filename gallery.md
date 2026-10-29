---
layout: default
title: 图集
permalink: /gallery/
---

## 漫画

<ul class="post-list">
  <li><a href="{{ '/gallery/manga/' | relative_url }}">复活赛</a></li>
</ul>

---

## 待施工

<ul class="post-list">
{% for post in site.categories.gallery %}
<li>
  <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  <a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}
</ul>


