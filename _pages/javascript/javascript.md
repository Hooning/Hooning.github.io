---
layout: "pages"
title: "Posts related to Javascript"
permalink: /javascript/
---

## Javascript Basics

<ul>
  {% for post in site.posts %}
    {% if post.tags[0] == "javascript" and post.tags[1] == "basics" %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
  {% endfor %}
</ul>
