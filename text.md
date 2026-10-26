---
layout: default
title: 文字
permalink: /text/
---
<ul class="post-list">
{% for post in site.posts %}
<li><span class="date">{{ post.date | date: "%Y-%m-%d" }}</span> <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
