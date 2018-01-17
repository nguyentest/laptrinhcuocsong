---
layout: default
---

fsdafsdafsdafsdaf

{% for post in paginator.posts %}
<article class="post" itemscope itemtype="http://schema.org/Article">
  <h1 itemprop="name"><a itemprop="url" href="{{ site.site_url }}{{ post.url }}" title="{{ post.title | xml_escape }}" >{{ post.title | xml_escape }}</a></h1>
  {% if post.thumbnail %}
  <a href="{{ post.url }}"><img itemprop="image" src="{{ site.site_url }}/images/{{ post.thumbnail }}" title="{{ post.title | xml_escape }}" alt="{{ post.title | xml_escape }}" class="post_thumbnail"></a>
  {% else %}
  <a href="{{ post.url }}"><img itemprop="image" src="{{ site.site_url }}/images/thumbnail_default.png" alt="{{ post.title  | xml_escape }}" class="post_thumbnail"></a>
  {% endif %}
  <div class="excerpt" itemprop="description">
    {{ post.excerpt }}
  </div>
  <div class="clear"></div>
</article>
{% endfor %}

<div class="pagination">
  {% if paginator.previous_page %}
  <a href="{{ paginator.previous_page_path }}" class="button prev-link">&laquo; Trang trước</a>
  {% endif %}
  {% if paginator.next_page %}
  <a href="{{ paginator.next_page_path }}" class="button next-link">Trang sau &raquo;</a>
  {% endif %}
  <div class="clear"></div>
</div>
