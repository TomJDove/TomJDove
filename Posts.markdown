---
layout: page
title: "Blog"
permalink: /posts
---

As a way of developing my data and writing skills, I've decided to undertake little projects and writing about my findings.

In my first article, I look into the ArXiv metadata to see what it says about gender equality in mathematics.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
