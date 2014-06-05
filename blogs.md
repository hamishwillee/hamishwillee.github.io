---
layout: page
title: Blogs
rss: true
permalink: /blog/
---

<div class="posts">
<ul>
    {% for post in site.posts %}
      {% if post.tags contains 'draft' %}<!--do nothing -->{% else %}
       <li> <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a><span class="small-post-date"> - {{ post.date | date: "%b %-d, %Y" }}</span>
{% if post.tags != empty %} <div class="tag-icon-image"> {% for tag in post.tags %} <div class="tag-link"><a href="{{ site.baseurl }}/tags#{{ tag }}&tag={{ tag | uri_escape }}">{{ tag }}</a></div> {% endfor %}</div>{% endif %} 
<!-- </div> --></li> 
      {% endif %} 
    {% endfor %} 
</ul></div>



   






