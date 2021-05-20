---
layout: "pages"
title: "Posts related to Java"
permalink: /java/
---

## Java Basics
<ul>
  {% for post in site.posts %}
    {% if post.tags[0] == "java" & post.tags[1] == "basics" %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
  {% endfor %}
</ul>