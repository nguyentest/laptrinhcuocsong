---
layout: default
title: Danh mục
permalink: danhmuc.html
---
<h1>2</h1>
<div class="posts">
{% for category in site.categories %}
  <li><a name="{{ category }}">{{ category}}</a>
    <ul>
    {% for posts in category %}
    a
      {% for post in posts %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    {% endfor %}
    </ul>
  </li>
{% endfor %}
</div>