---
layout: default
title: Chuyện lập trình
permalink: chuyen-lap-trinh.html
excerpt: Các bài viết liên quan đến kỹ thuật, lập trình, các vấn đề công nghệ, thủ thuật
---


{% assign categories = site.categories | sort %}
<div id="index">

{% for category in categories %}

	{% if category[0] == "Chuyện lập trình" %}
	<div class="category_detail">
		<h1>{{ category[0] }}</h1>
		<p>Chuyện lập trình - là chuyên mục mà một thằng coder viết về các vấn đề liên quan đến kỹ thuật, lập trình, những gì hắn đã học được trong quá trình cày cuốc của mình.</p>
	</div>
		{% for post in site.posts %}
		{% if post.categories contains category[0] %}

		<article class="post" itemscope itemtype="http://schema.org/Article">
		  <h1 itemprop="name"><a itemprop="url" href="{{ site.site_url }}{{ post.url }}" title="{{ post.title | xml_escape }}" >{{ post.title | xml_escape }}</a></h1>
		  {% if post.thumbnail %}
		  <a href="{{ post.url }}"><img itemprop="image" src="{{ site.baseurl }}images/{{ post.thumbnail }}" alt="{{ post.title | xml_escape }}" class="post_thumbnail"></a>
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

