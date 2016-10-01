---
layout: default
title: Danh mục bài viết
permalink: /danh-muc-bai-viet.html
---


{% assign categories = site.categories | sort %}
<div id="index">

{% for category in categories %}
<a name="{{ category}}"></a><h2>{{ category}}</h2>
{% assign sorted_posts = site.posts | sort: 'title' %}
{% for post in sorted_posts %}
{%if post.categories contains category[0]%}

  <h3>
  <a href="{{ site.url }}{{site.baseurl}}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </h3>
{%endif%}
{% endfor %}

{% endfor %}
</div>

