---
layout: default
title: Danh mục bài viết
permalink: danh-muc-bai-viet.html
---


{% assign categories = site.categories | sort %}
<div id="index">

{% for category in categories %}
	{% if category[0] == "Học-lập-trình" %}
	echo hoc lap trinh
		<a name="{{ category[0] }}"></a><h2>{{ category[0] }}</h2>
		{% assign sorted_posts = site.posts | sort: 'title' %}
		{% for post in sorted_posts %}
		{% if post.categories contains category[0] %}

		  <h3>
		  <a href="{{ site.url }}{{site.baseurl}}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
		  </h3>
		{%endif%}
		{% endfor %}
	{% endif %}

{% endfor %}
</div>

