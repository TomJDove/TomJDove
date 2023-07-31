---
layout: page
title: "Blog"
permalink: /posts
---

As a way of developing my data and writing skills, I've decided to undertake little projects/investigations and writing about my findings.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
