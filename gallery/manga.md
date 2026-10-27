---
layout: default
title: manga
---

<a class="back-btn" href="{{ '/gallery/' | relative_url }}">← 返回</a>
<div class="spread" id="spread"></div>

<div class="reader-bar">
  <button onclick="prev()">← 上一页</button>
  <span id="page-num"></span>
  <button onclick="next()">下一页 →</button>
</div>

<script>

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
    
    html = `<img src="${pages[single]}">`;
    numEl.textContent = `${single + 1} / ${pages.length}`;
  } else if (step === 0) {

    html = `<img src="${pages[0]}">`;
    numEl.textContent = `1 / ${pages.length}`;
  } else {

    const right = 2 * step - 1;
    const left = 2 * step;
    html = `<img src="${pages[right]}">`;
    if (left < pages.length) {
       html = `<img src="${pages[left]}">` + html;
    }
    numEl.textContent = `${right + 1}~${Math.min(left + 1, pages.length)} / ${pages.length}`;
  }
  spreadEl.innerHTML = html;


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

  
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight') next();
  if (e.key === 'ArrowLeft') prev();
});


spreadEl.addEventListener('click', e => {
  const x = e.clientX / window.innerWidth;
  if (x > 0.5) next(); else prev();
});

render();
</script>
