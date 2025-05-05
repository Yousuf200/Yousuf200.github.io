---
layout: default
title: Blog
permalink: /blog/
---

<h1>🧱 Minecraft Blog</h1>
<p>Welcome to the Minecraft adventures blog! Read about crafting, building, redstone tricks, and more.</p>

<h2>Recent Posts</h2>

<!-- <ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <p>{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul> -->

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <p>{{ post.excerpt | split: '\n' | first }}</p>  <!-- This shows only the first line -->
    </li>
  {% endfor %}
</ul>


