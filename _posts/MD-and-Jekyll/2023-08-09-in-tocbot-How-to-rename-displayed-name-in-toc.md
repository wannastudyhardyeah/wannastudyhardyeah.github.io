---
title: tocbot에서 ToC에 표출되는 이름 변경하는 방법
author: wannastudyhardyeah
date: 2023-08-09 01:01:30 +0800
categories: [BLOG]
tags: [BLOG, jekyll, toc, tocbot]
math: true
mermaid: true

---
<blockquote cite="https://github.com/tscanlin/tocbot/blob/d9f5813e4440309c474157d2bbda8426bc9b6166/src/js/default-options.js">
  <p>
    Expects a string and returns the modified label to display.<br>
    Additionally, <b style="color: black;">the attribute `data-heading-label`</b> may be used on a heading to specify a shorter string to be used in the TOC.
  </p>
  <hr width="50%">
  <p>출처: <a href="https://github.com/tscanlin/tocbot/blob/d9f5813e4440309c474157d2bbda8426bc9b6166/src/js/default-options.js" target="_blank">tocbot 깃허브의 ``tocbot/src/js/default-options.js`` 中</a></p>
</blockquote>
<span style="color: red; font-size: 25px"><b><code class="language-plaintext highlighter-rouge" style="font-size: 25px">data-heading-label</code></b>을 통해 변경하면 된다!!!!</span><br>

<b style="font-size: 18px">예시</b><br>
```HTML
<h3 id="it-is-never-displayed" data-heading-label="only for toc">only for post</h3>
```
<h3 id="it-is-never-displayed" data-heading-label="only for toc">only for post</h3>

