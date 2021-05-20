---
layout: "pages"
title: "Posts related to Angular"
permalink: /angular/
---

## Angular Basics
<ul>
  {% for post in site.posts %}
    {% if post.tags[0] == "angular" & post.tags[1] == "basics" %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
  {% endfor %}
</ul>