---
layout: page
title: Tags
permalink: /tags/
---

Tags: {% for tagitem in site.tags %} [{{ tagitem[0] }}](#{{ tagitem[0] }}) {% endfor %}


<hr>

{% for tagitem in site.tags %}

<div id="{{ tagitem[0] }}">
<h2> {{ tagitem[0] }} </h2>
 <ul>
  {% for post in site.posts %}
 
      {% if post.tags contains tagitem[0] %}
         
        <li>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a><span class="small-post-date"> - {{ post.date | date: "%b %-d, %Y" }}</span>
          {% if post.tags != empty %} <div class="tag-icon-image"> {% for tag in post.tags %} <div class="tag-link"><a href="#{{ tag }}">{{ tag }}</a></div> {% endfor %}</div>{% endif %} 
         </div>
</li>
      {% endif %}

  {% endfor %}
</ul>

</div>
{% endfor %}




