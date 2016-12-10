---
layout: default
title: Danh mục bài viết
permalink: chuyen-ben-le.html
---


{% assign categories = site.categories | sort %}
<div id="index">

{% for category in categories %}

	{% if category[0] == "Chuyện bên lề" %}
	<div class="category_detail">
		<h1>{{ category[0] }}</h1>
		<p>Chuyện bên lề - là chuyên mục viết về mọi thứ liên quan đến cuộc sống của một thằng coder</p>
	</div>
		{% assign sorted_posts = site.posts | sort: 'title' %}
		{% for post in sorted_posts %}
		{% if post.categories contains category[0] %}

		<article class="post" itemscope itemtype="http://schema.org/Article">
  <h1 itemprop="name"><a href="{{ post.url }}" title="{{ post.title }}" >{{ post.title }}</a></h1>
  {% if post.thumbnail %}
  <a href="{{ post.url }}"><img src="{{ site.baseurl }}images/{{ post.thumbnail }}" alt="{{ post.title }}" class="post_thumbnail"></a>
  {% endif %}
  <div class="excerpt" itemprop="description">
    {{ post.excerpt }}
  </div>
  <div class="clear"></div>
</article>

		{%endif%}
		{% endfor %}
	{% endif %}

{% endfor %}
</div>

