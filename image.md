---
layout: default
title: image
permalink: /image/
---

<h2>漫画</h2>
<ul class="post-list">
  <li><a href="{{ '/image/manga/' | relative_url }}">我的漫画（点进去阅读）</a></li>
</ul>

<h2>图集</h2>
<ul class="post-list">
{% for post in site.categories.image %}
<li>
  <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  <a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}
</ul>


