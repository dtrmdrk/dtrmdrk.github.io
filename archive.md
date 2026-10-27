---
layout: default
title: 索引
permalink: /archive/
---

<input type="text" id="search" placeholder="请输入关键词…" autocomplete="off">
<div id="results"></div>

<script>

const posts = [
  {% for post in site.posts %}
  {
    title: {{ post.title | jsonify }},
    url: {{ post.url | relative_url | jsonify }},
    date: {{ post.date | date: "%Y-%m-%d" | jsonify }},
    categories: {{ post.categories | jsonify }},
    tags: {{ post.tags | jsonify }},
    excerpt: {{ post.excerpt | strip_html | truncate: 80 | jsonify }}
  },
  {% endfor %}
];

const input = document.getElementById('search');
const results = document.getElementById('results');

function render(list) {
  if (!input.value.trim()) {
    results.innerHTML = '<p style="color: var(--meta);"></p>';
    return;
  }
  if (list.length === 0) {
    results.innerHTML = '<p style="color: var(--meta);">没有找到相关文章。</p>';
    return;
  }
  results.innerHTML = '<ul class="post-list">' + list.map(p => `
    <li>
      <span class="date">${p.date}</span>
      <a href="${p.url}">${p.title}</a>
    </li>`).join('') + '</ul>';
}

function search() {
  const q = input.value.trim().toLowerCase();
  render(posts.filter(p =>
    p.title.toLowerCase().includes(q) ||
    p.categories.join(' ').toLowerCase().includes(q) ||
    p.tags.join(' ').toLowerCase().includes(q) ||
    p.excerpt.toLowerCase().includes(q)
  ));
}

input.addEventListener('input', search);
render(posts);
</script>
