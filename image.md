---
layout: default
title: image
permalink: /image/
---
<ul class="post-list">
{% for post in site.categories.image %}
<li>
  <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  <a href="{{ post.url }}">{{ post.title }}</a>
</li>
{% endfor %}
</ul>
