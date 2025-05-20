---
layout: post
title: "Copy code test 3"
date: 2025-05-20T09:56:01.906Z
---

this is the content of the post

<div style="position: relative; background: #1e1e1e; padding: 1em; border-radius: 8px; font-family: monospace; white-space: pre-wrap; word-wrap: break-word; color: #f8f8f2; border: 1px solid #444;">
  <button onclick="copyCodeBlock(this)" style="position: absolute; top: 10px; right: 10px; padding: 4px 8px; font-size: 0.8em; background: #444; color: #fff; border: none; border-radius: 4px; cursor: pointer;">Copy</button>
  <code>this is where the code is and the hope the copy code works</code>
</div>

&lt;script&gt;
function copyCodeBlock(button) {
  const code = button.nextElementSibling.innerText;
  navigator.clipboard.writeText(code).then(() => alert("Copied!"));
}
&lt;/script&gt;