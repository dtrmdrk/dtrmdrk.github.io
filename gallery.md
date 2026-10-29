---
layout: default
title: 图集
permalink: /gallery/
---

<ul class="post-list">
{% for post in site.categories.gallery %}
<li>
  <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  <a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}
</ul>


