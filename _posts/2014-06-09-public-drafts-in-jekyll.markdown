---
layout: post
title:  "Public draft posts in a Github-Jekyll blog"
date:   2014-06-11 20:55:32
author: Hamish Willee
description: This shows how drafts can be public but hidden and marked as clearly unpublished on a Jekyll blog.
tags:
- jekyll
---

This post shows how to build draft posts into the published version of a Jekyll site, but hide them from casual observation. 

# Introduction

Drafts are posts that aren't yet ready to be published. Jekyll's does not generate pages for draft posts by default, but instead provides a special preview build option. 

In many cases draft posts are not *confidential*, the author simple doesn't wish to distract readers with incomplete ideas. It is therefore reasonable that drafts posts are generated in the site HTML, as long as they aren't obtrusive. 

This post explains one approach for creating *public drafts*. The approach has the following benefits over Jekyll's [official support for drafts](#Standard Jekyll process for creating drafts):

* Drafts can be previewed and shared with reviewers on the live site - there is no need for a separate build.
* Published draft files do not need to be renamed or moved - you just need to remove the draft variable and add the current date variable. 
* Bloggers using Github's inbuilt Jekyll publishing do not need a copy of Jekyll to preview posts.


# Standard Jekyll process for creating drafts

Jekyll's official support for drafts is covered in [Working with Drafts](http://jekyllrb.com/docs/drafts/). Jekyll expects you to put your *undated* draft posts in a folder **_drafts** in your site root. 
{% highlight bash %}
|-- _drafts/
|   |-- a-draft-post.md
{% endhighlight %}
To preview the drafts you build/serve the site using `--drafts` command. Jekyll then builds the drafts with the current date so that they are easy to find at the top of your blog listings.
{% highlight bash %}
jekyll serve --drafts
{% endhighlight %}
    
When you're ready to publish you simply move the file to the **_posts** folder and rename it to include the current date. 
{% highlight bash %}
|-- _posts/
|   |-- YYYY-MM-DD-a-draft-post.md
{% endhighlight %}


<div class="message"><b>Note: </b><a href="https://github.com/jekyll/jekyll/blob/master/features/drafts.feature">drafts.feature</a> provides information about another feature of the drafts system. A draft with <tt>published: false</tt> in the frontmatter will not be published even using the <tt>--drafts</tt> option.
</div>

# Public draft posts

## Marking posts as drafts

To mark a post as draft, use a variable in the [front matter](http://jekyllrb.com/docs/frontmatter/). This could be a separate variable as shown below:
{% highlight bash %}
draft: true
{% endhighlight %}
However for this site I decided to build onto the [existing tag system]({% post_url 2014-06-06-tags-in-jekyll-without-plugins %}), and represent drafts using a tag.
{% highlight bash %}
tags:
- draft
{% endhighlight %}

<div class="message"><b>Note: </b>Don't apply any other tags until the page is published. This ensures that drafts pages do not appear in non-draft tag lists.
</div>

## Conditionally hiding and displaying draft content

To hide or display drafts you can use [Liquid operators](http://docs.shopify.com/themes/liquid-basics) and test for the existance of the variable or tag. The code below shows a conditional test for whether a particular page contains the draft tag.
{% highlight html %}
{% raw %}
{% if post.tags contains 'draft' %}
  <!-- This is a draft. Allow blog to be displayed in draft blog lists. Use in blog page layout to display a warning that the page is a draft. -->
{% else %} 
  <!-- This is not a draft. Allow post to be displayed in blog lists and RSS feed --> 
{% endif %}
{% endraw %}
{% endhighlight %}

You would then use the conditional code in the:

* blog archive page and RSS feeds to remove draft posts from the listings.
* post layout to automatically add a clear watermark to draft posts.
* post layout to add `noindex` and `nofollow` metatdata so that the blog post won't be indexed by search engines
* **Drafts.html** page to list drafts. Note that this drafts page might be hidden from sitemaps and your navigation. My implementation does not use this file, but instead displays drafts in the **tags.html** file.


## Naming your post file

Posts are automatically generated if they have the correct date-format in their filename and they are present in the **_posts** directory.
{% highlight bash %}
|-- _posts/
|   |-- YYYY-MM-DD-a-draft-post.md
{% endhighlight %}

You must have a date, and when creating file there is no reason not to use the current draft-create date. As you will see in the next section, the date used for the post once it is published can be overridden in the frontmatter. 

## Publishing the post

In order to publish the post, you simply update the page frontmatter: remove the `draft` variable or tag, add any other tags needed by the article, and finally add a new date variable for the file (this becomes the published date).
{% highlight bash %}
date:   2014-06-09 20:55:32
{% endhighlight %}

The post will now appear in the main blog feeds and RSS, and will no longer have the draft warning displayed.


# Summary

Publically publishing drafts while making them unobtrusive is easy to implement. Once implemented you can preview drafts and and share drafts for review on the live site. It is also easier to finally publish a draft post, because this is simply a change to the front-matter (rather than moving and renaming a file).

You can check out the [example draft post here]({% post_url 2014-06-05-Example-draft--blog %}), and link to other blogs through it's `draft` tag.
