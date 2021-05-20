---
layout: posts
date: 2021-03-19 15:54
title: "[TEST] Template post!"
categories: test template
tags: ['Basic', 'Test']
summary: "This is the test post"
permalink: "/test/:title.html"
published: false
---
# Hello this is the test post

## index of posts
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

## tags and posts
{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}

## Code examples
```
function helloWorld() {
    return "Hello World!"
}
```
