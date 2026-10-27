---
layout: default
title: manga
permalink: /gallery/manga/
reader: true
---

<a class="back-btn" href="{{ '/gallery/' | relative_url }}">← 返回</a>
<div class="spread" id="spread"></div>

<div class="reader-bar">
  <button onclick="prev()">← 上一页</button>
  <span id="page-num"></span>
  <button onclick="next()">下一页 →</button>
</div>

<script>
// Jekyll 构建时扫描 assets/manga/ 里的所有图片，按文件名排序
const pages = [
  {% assign files = site.static_files | where_exp: "f", "f.path contains '/manga/'" | sort: "name" %}
  {% for f in files %}"{{ f.path }}",
  {% endfor %}
];

const spreadEl = document.getElementById('spread');
const numEl = document.getElementById('page-num');
const isMobile = window.matchMedia('(max-width: 700px)').matches;

let step = 0;
let single = 0;

function stepTotal() { return 1 + Math.floor((pages.length - 1) / 2); }

function render() {
  let html = '';
  if (isMobile) {
    // 手机：单页模式
    html = `<img src="${pages[single]}">`;
    numEl.textContent = `${single + 1} / ${pages.length}`;
  } else if (step === 0) {
    // 封面单独显示
    html = `<img src="${pages[0]}">`;
    numEl.textContent = `1 / ${pages.length}`;
  } else {
    // 双页跨页：右页 = 2*step-1，左页 = 2*step（日式右翻）
    const right = 2 * step - 1;
    const left = 2 * step;
    html = `<img src="${pages[right]}">`;
    if (left < pages.length) {
      html = `<img src="${pages[left]}">` + html;
    }
    numEl.textContent = `${right + 1}~${Math.min(left + 1, pages.length)} / ${pages.length}`;
  }
  spreadEl.innerHTML = html;

  // 预加载下一页
  const nextIdx = isMobile ? single + 1 : 2 * step + 1;
  if (nextIdx < pages.length) new Image().src = pages[nextIdx];
}

function next() {
  if (isMobile) { if (single < pages.length - 1) single++; }
  else if (step < stepTotal() - 1) step++;
  render();
}
function prev() {
  if (isMobile) { if (single > 0) single--; }
  else if (step > 0) step--;
  render();
}

// 键盘翻页
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight') next();
  if (e.key === 'ArrowLeft') prev();
});

// 点击图片右半=下一页，左半=上一页
spreadEl.addEventListener('click', e => {
  const x = e.clientX / window.innerWidth;
  if (x > 0.5) next(); else prev();
});

render();
</script>
