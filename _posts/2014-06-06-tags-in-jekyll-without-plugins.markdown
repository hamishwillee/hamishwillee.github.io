---
layout: post
title:  "Tags in Jekyll without using plugins"
date:   2014-06-06 20:55:32
author: Hamish Willee
description: Find out how to support tags in Jekyll blogs without using plugins. This allows automatic rebuilding of index by Github's inbuilt Jekyll.
tags:
- jekyll
---

This post shows how to support tags in jekyll without using plugins. This means you can have tags in blog sites that are built automatically using Github's inbuilt Jekyll.

# Introduction 


Jekyll has rudimentary support for tags. You can add tags to pages and specify how, if present, they are to displayed in your layouts. You can also list all tags that have been applied to all *posts* across the site. 

What isn't so obvious is how to get (and link to) a list of all topics with a particular tag.

The [common approach](http://charliepark.org/tags-in-jekyll/) for supporting tags is to use a custom plugin to create a separate index page for each tag. Unfortunately this means that you can't use automatic publishing of your sources when you create a new post, because Github's version of Jekyll won't run custom plugins. Instead you will have to manually rebuild your sources and push the new site to the publishing repository.

However there is no real necessity to have separate index files for each tag, which is why a plugin are needed. The alternative is to have a *single* index page with a separate heading, anchor and list of blog posts for each tag. Linking to the correct index from a tag is then as simple as opening the index page with the correct anchor.

This approach is easy to implement, and since it does not use plugins, Github will automatically publish the updated index whenever you add a new post. 

# Adding tags to a page

Tags are added to the *tags* variable in the page/post [front-matter](http://jekyllrb.com/docs/frontmatter/):

{% highlight javascript %}
---
layout: post
title:  "Welcome to my Jekyll blog"
tags:
- jekyll
- other-tag
- example
---
{% endhighlight %}

The tags can be accessed in pages and layouts using the [Liquid variable](http://docs.shopify.com/themes/liquid-basics) `page.tags`. You can also get a list of all the tags that have been applied to all *posts* using the `site.tags` variable.

<div class="message"><b>Note: </b><i>site.tags</i> only includes the tags defined in <i>posts</i>, not <i>pages</i></div>


# Tags index page

Create a tags page for the index: <i>Tags.md</i>. The page needs two elements:

* A list of all the tags on the site, for easy navigation
* A heading and anchor for each of the tags, containing the list of tagged articles.

The list of tags on the site can be obtained by iterating through the `site.tags` variable using a Liquid [for-loop](http://docs.shopify.com/themes/liquid-basics/for-loops). Note that each iteration returns an array, and the tag is the first item: `tagitem[0]`.

{% highlight html %}
Tags: 
{{ "{% for tagitem in site.tags  " }}%} 
  [{{ "{{  tagitem[0] " }}}}](#{{ "{{ tagitem[0] " }}}}) 
{{ "{% endfor " }}%}
{% endhighlight %}

<div class="message"><b>Note: </b>The second item in the array returned by iterating <i>site.tags</i> is the post content. Unfortunately this is particularly useless, as it contains all the text in all the articles that have the tag - but without any separators or titles. There is no way to just get the list of titles or the list of <b>post</b> objects using this variable.</div>

To create the heading and anchor for each tag we again iterate the `site.tags`. Under each heading we iterate through all the site posts, listing only those which [contain](http://docs.shopify.com/themes/liquid-basics/contains) the current tag. 

{% highlight html %}
<!-- iterate through all tags on the site --> 
{{ "{% for tagitem in site.tags " }}%} 

<!-- for each tag, create an anchor by using the tag name as an id --> 
<div id="{{ "{{ tagitem[0] " }}}}">  
<h2> {{ "{{ tagitem[0] " }}}} </h2>  <!-- for create a heading --> 

 <ul> <!-- create the list of posts -->
 <!-- iterate through all the posts on the site --> 
 {{ "{% for post in site.posts " }}%} 
      <!-- list only those which contain the current tag --> 
      {{ "{% if post.tags contains tagitem[0] " }}%} 
         
        <li>
           <div class="tag-icon-image">
             <!-- iterate and list the tags for the current post --> 
             {{ "{% for tag in post.tags " }}%} 
                <div class="tag-link"><a href="#{{ "{{ tag " }}}}">{{ "{{ tag " }}}}</a></div> {{ "{% endfor " }}%}</div>
             {{ "{% endif " }}%} 
           </div>
        </li>

      {{ "{% endif " }}%}
  {{ "{% endfor " }}%}
</ul>

</div>
{{ "{% endfor " }}%}
{% endhighlight %}

Finally, when we list each post, we can iterate through its tags and list them with the title. For this page the URL we create is a local link within the page to an anchor for the tag - e.g. #jekyll.

Note that the code above also contains various HTML elements that are used for styling.

# Updating layouts
The layouts need to be updated to automatically display tags if they are defined for the current page. This can be done in the **posts.html** layout near the heading. The tags are displayed by iterating the `page.tags` variable. Note below that in this case we link to **tags.html#current-anchor**.

{% highlight html %}
<!-- only display tag "infrastructure" if there are tags -->
{{ "{% if page.tags != empty " }}%} 
 <div class="tag-icon-image"> 
    <!-- iterate through tags in the current page using page.tags variable -->
    {{ "{%  for tag in page.tags  " }}%} 
      <div class="tag-link">
       <!-- link to appropriate tag anchor in tags.html -->
       <a href="{{ site.baseurl }}/tags#{{ "{{ tag " }}}}">{{ "{{ tag " }}}}</a>
      </div> 
    {{ "{%  endfor " }}%}
 </div>
{{ "{%  endif  " }}%}
{% endhighlight %}


# Adding tags to blog listings

Adding tags to blog listing is virtually the same as adding them in the tag index. Iterate through `site.posts` using a for loop, then access the tags for each page using its `tags` variable. 

{% highlight html %}
<div class="posts">
  <ul>
    {{ "{% for post in site.posts " }}%}
       <li> 
       <a class="post-link" href="{{ "{{ post.url | prepend: site.baseurl " }}}}">{{ "{{ post.title " }}}}</a><span class="small-post-date"> - {{ "{{ post.date | date: "%b %-d, %Y" " }}}}</span>
           {{ "{% if post.tags != empty " }}%} 
              <div class="tag-icon-image"> 
                {{ "{% for tag in post.tags " }}%} 
                   <div class="tag-link"><a href="{{ "{{ site.baseurl " }}}}/tags#{{ "{{ tag | uri_escape " }}}}">{{ "{{ tag " }}}}</a></div> 
                {{ "{% endfor " }}%}
              </div>
            {{ "{% endif " }}%} 
       </li> 
    {{ "{% endfor " }}%} 
  </ul>
</div>

{% endhighlight %}


# Next steps

One improvement might be to add JavaScript to the `tags.md` which would hide all sections except the one for the current tag. I am in two minds on this - it is useful to see all tags present and having the others is not overly distracting.

# Summary

The "single page tag index" approach is used on this site. I particularly like that I don't need to move away from automatic Jekyll generation of the site in order to support tagging. 

<!-- http://stackoverflow.com/questions/3426182/how-to-escape-liquid-template-tags USEFUL LINK FOR ESCAPING LIQUID tags -->

