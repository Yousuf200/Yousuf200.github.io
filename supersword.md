---
layout: default
title: Super Sword
permalink: /supersword/
---

<h1>🧱 Super Sword ⚔️</h1>
<p>Welcome to the Minecraft adventures blog! Learn about commands and more.</p>

<div style="position: relative; background: #1e1e1e; padding: 1em; border-radius: 8px; font-family: monospace; white-space: pre-wrap; word-wrap: break-word; color: #f8f8f2; border: 1px solid #444;">
  <button onclick="copyCode()" style="position: absolute; top: 10px; right: 10px; padding: 4px 8px; font-size: 0.8em; background: #444; color: #fff; border: none; border-radius: 4px; cursor: pointer;">Copy</button>
  <code id="command-block">/give &lt;Your Name&gt; netherite_sword{Unbreakable:1,Enchantments:[{id:vanishing_curse,lvl:1},{id:mending,lvl:1},{id:sharpness,lvl:255},{id:smite,lvl:255},{id:sweeping_edge,lvl:255},{id:unbreaking,lvl:255},{id:bane_of_arthropods,lvl:255},{id:fire_aspect,lvl:255},{id:looting,lvl:255},{id:knockback,lvl:255}],display:{Name:'{"text":"Eternity Sword","color":"red","underlined":true,"bold":true,"italic":true}',Lore:['{"text":"The ultimate blade"}']},SkullOwner:{Id:[I;-1737552557,1684161468,-2105557318,-1694640140]}} 1</code>
</div>

<script>
function copyCode() {
  const code = document.getElementById("command-block").innerText;
  navigator.clipboard.writeText(code).then(() => alert("Copied!"));
}
</script>

<video width="640" height="360" controls>
  <source src="/assets/videos/door.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

