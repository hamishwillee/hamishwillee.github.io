---
layout: page
title: Blogs
rss: true
permalink: /blog/
---

  <div class="posts">
    {% for post in site.posts %}
      <div class="postblock">
<a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a><span class="post-date"> - {{ post.date | date: "%b %-d, %Y" }}</span>
{% if post.tags != empty %} <div class="tag-icon-image"> {% for tag in post.tags %} <div class="tag-link"><a href="{{ site.baseurl }}/tags#{{ tag }}&tag={{ tag | uri_escape }}">{{ tag }}</a></div> {% endfor %}</div>{% endif %} 
</div> {% endfor %} </div>




