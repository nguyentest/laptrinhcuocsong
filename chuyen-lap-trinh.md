---
layout: default
title: Chuyện lập trình
permalink: chuyen-lap-trinh.html
---


{% assign categories = site.categories | sort %}
<div id="index">

{% for category in categories %}

	{% if category[0] == "Chuyện lập trình" %}
	<div class="category_detail">
		<h1>{{ category[0] }}</h1>
		<p>Chuyện lập trình - là chuyên mục mà một thằng coder viết về các vấn đề liên quan đến kỹ thuật, lập trình, những gì hắn đã học được trong quá trình cày cuốc của mình.</p>
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

