---
layout: default
title: 文字
permalink: /text/
---
<ul class="post-list">
{% for post in site.categories.文字 %}
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


<p>调试：全站文章 {{ site.posts.size }} 篇，文字分类 {{ site.categories.文字.size }} 篇</p>
