---
layout: default
title: 索引
permalink: /archive/
---
<ul class="post-list">
{% for post in site.posts %}
<li><span class="date">{{ post.date | date: "%Y-%m-%d" }}</span> <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
