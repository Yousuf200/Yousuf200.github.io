---
layout: home
title: "Welcome to My Blog"
---

**بِسْمِ ٱللَّٰهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ**  

Welcome to my blog! This is my journey of finding the Path.

## Recent Posts
{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}