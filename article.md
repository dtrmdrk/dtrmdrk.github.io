---
layout: default
title: 文章
permalink: /article/
---
<ul class="post-list">
{% for post in site.categories.article %}
<li>
  <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  <a href="{{ post.url }}">{{ post.title }}</a>
  <span class="tags">
    {% for tag in post.tags %}
    <span class="tag">{{ tag }}</span>
    {% endfor %}
  </span>
</li>
{% endfor %}
</ul>


