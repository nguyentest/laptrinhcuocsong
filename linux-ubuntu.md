---
layout: default
title: Linux - ubuntu
permalink: linux-ubuntu.html
---


{% assign categories = site.categories | sort %}
<div id="index">

{% for category in categories %}

	{% if category[0] == "Linux - ubuntu" %}
	<div class="category_detail">
		<h1>{{ category[0] }}</h1>
		<p>Linux - ubuntu là chuyên mục mà một thằng coder viết về hệ điều hành hắn yêu thích, chia sẻ mọi thứ hắn biết về ubuntu và linux.</p>
	</div>
		{% for post in site.posts %}
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

