---
layout: post
title:  "Welcome to my Jekyll blog"
tags:
- jekyll
---


Welcome to my brand-spanking-new [Jekyll-powered](http://jekyllrb.com/) blog, hosted for *free* on [Github pages](https://pages.github.com/). After years of blogging on company blogs, I've decided it is time I had my own place to talk more generally about communities, writing, and anything else that interests me. 

The main reason I've considered Jekyll for the blog (rather than WordPress), is that it will be used for the documentation platform in an upcoming technical writing job. Creating a blog has been a very good way to get up and running quickly! It has also been a good way to get familiar with [Liquid](http://docs.shopify.com/themes/liquid-basics), and to refresh my CSS and JavaScript. 

For those that are interested, this post provides a brief overview of Jekyll, my blog, and other Jekyll-based blogging frameworks. 

<div class="message">Note: The only really <i>clever</i> things I did (i.e. not covered by other articles on the Internet) were to add a new form of tagging, better management for drafts, along with a link in the site bar for raising bugs. I'll discuss those in separate blogs.</div>

<img alt="Jekyll official logo" src="http://jekyllrb.com/img/logo-2x.png" />

# What is Jekyll?
[Jekyll](http://jekyllrb.com/) is an open-source static HTML generator tool which builds static HTML pages from plain text files written in wiki syntax ([Markdown](http://daringfireball.net/projects/markdown/) or [Textile](http://textile.sitemonks.com/)). The content, structure and appearance of the site can be controlled using the [Liquid](http://docs.shopify.com/themes/liquid-basics) templating language, along with HTML and CSS. The tool also has support for various types of plugins, which can further customise the behaviour and output of the generated content.

While Jekyll can be used for generating any sort of HTML site, it does have features specifically to support blogging, and comes with a default blog project.


# Is Jekyll for me?

What I really like about Jekyll is that you write your content in wiki sytnax. This is easier to format than HTML, and results in more predictable output than WYSIWYG editors. The biggest benefit is that with limited (but adequate) style options, authors tend to concentrate on the conent and structure.

Other common reasons given by bloggers for using Jekyll are listed below:

* Output is "static HTML", which means that it is lightweight and can be hosted anywhere: Github, DropBox, or even a USB stick (unlike WordPress, which is an application running on top of an operating system). 
* Posts/pages can be written in Markdown, which is much easier to write, preview and maintain than HTML.
* The site sources can be hosted on Github, getting a lot of free space and free backup.
* The site output can be hosted on Github pages for free. Support for Jekyll is "baked into" Github pages so that source stored in the correct location is automatically converted by Jekyll in a "safe mode" (with limited plugins). A project that requires unsupported plugins can be hosted anywhere and then the generated output can be copied to the Github pages.
* The site layout and appearance is completely up to the developer. This is a two-edge sword - you *will* spend ages playing around with the CSS to get it to look right. On the other hand, you will get it to look right, and on all browsers and devices!
* Generally speaking, the files used for posts contain only markup (not style). This means that you can change your "Theme" without having to go back and update any of your content.


Having created my blog I'd say that the biggest disadvantage is that you do need to have some technical skills to run the tool, configure and host your blog:

* Jekyll runs *most reliably* on Linux and requires the Ruby programming environment. Windows is supported, but as a second-class platform citizen. To address this I set up Ubuntu on a virtual machine and ran Jekyll/Ruby in that environment.
* Adding "common" features to the template provided by Jekyll is easy as there are great instructions on the web. What can be time consuming is making these features work with your site's CSS. 
* More generally, customising any appearance is time consuming unless you're very familiar with CSS. 
* You're responsible for your own backup. Storing your site on a Github repository is a good solution. 
* Blog text is not spell-checked or grammar-checked by default using gedit on Ubuntu. Note to self - find a good spell checker!

Some of the problems above have been reduced by frameworks like [Octopress](http://octopress.org/), which have support for theming and a community of theme-creators. 


# My site configuration

Originally I started with the default Jekyll blog project. The [Jekyll QuickStart](http://jekyllrb.com/docs/quickstart/) shows how to create this using the 'Jekyll new' command and start a local server to browse it. The main problem with this default blog is that it is missing many of the features you would commonly expect: *social widgets*, *tags*, *search*, *analytics*, and the ability to add *comments*. Most importantly, the CSS support for mobile devices was poor - the menu button responding to hover rather than "click".

The lack of adequate support for smaller screen sizes was a deal breaker for me. I chose instead to follow the example in the article [How I Created a Beautiful and Minimal Blog Using Jekyll, Github Pages, and poole](http://joshualande.com/jekyll-github-pages-poole/). Poole has a simple mobile-friendly design, and CSS which I could easily understand. In addition, it was created without any dependency on special plugins - which means that it can take advantage of Github's inbuilt support for Jekyll.

Globally I added a navbar, analytics, search bar, and a bottom bar with links to my social networking presence. I added site pages introduction, about me, blog archive, tag listing, and RSS feed. Almost everything I included was clearly explained in the articles:

* [Disqus - Jekyll installation instructions](http://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions)
* [Jekyll From Scratch - Extending Jekyll](http://pixelcog.com/blog/2013/jekyll-from-scratch-extending-jekyll/)
* [How I built my blog in one day](http://erjjones.github.io/blog/How-I-built-my-blog-in-one-day/)
* [How I Created a Beautiful and Minimal Blog Using Jekyll, Github Pages, and poole](http://joshualande.com/jekyll-github-pages-poole/) 

<div class="message">Tip: It is better put new functionality in separate <i>_include</i> files than to embed direct in <i>layouts</i>. This allows you to migrate custom functionality to a new site much more easily.</div>

It took more than [the single day suggested in this article](http://erjjones.github.io/blog/How-I-built-my-blog-in-one-day/), mostly because I spent so long modifying the CSS to get additional features to lay out the way I wanted. I am very happy with the results!

# Blogging with Github Pages - automatic vs. offline Jekyll

[Github Pages](http://pages.github.com) is a great (free) place to publish a Jekyll blog. Pages placed in your correctly named repostory (/*username*/*username*.github.io) are automatically published to the site *username.github.io*. Even better, Github runs Jekyll automatically on content in the respository, so your pages can be a Jekyll project.

The caveat here is that Github runs Jekyll in a "safe mode" (see [Using Jekyll with Pages](https://help.github.com/articles/using-jekyll-with-pages)) which runs only a small set of default plugins. This means that if your project depends on any custom plugins, they will not be run. In this case you can still use Jekyll, but you will need to have a separate repository for your sources, build them using your own copy of Jekyll, and then upload the final output to your publishing respository.

Plugins can be extemely useful. They can provide easier syntax for declaring special markup (for example, custom markup for adding "Notes" or support for embedding videos easily) and support features that would otherwise be hard on a static site (for example creating separate index pages for post tags). Popular Jekyll-based frameworks like Octopress use plugins to make the blogging process easier, so if you want to use them, the automatic publishing approach is not an option.

If you don't have to rely on plugins then you can work with new posts *direct in Github* - just create a new post and commit the change to automatically publish. This can be extremely handy if you're travelling, and don't want to have to bring your laptop with Git, Jekyll etc. 

Which option you use then really depends on *convenience*. I have selected the automatic option, because I am the only one using the blog so there is no great value in simplifying the syntax. I also like the ability to make small changes very easily, without having to rebuild the site.


# Other options: Octopress and the Jekyll Bootstrap

The [Jekyll Bootstrap](http://jekyllbootstrap.com/) also addresses many of the problems of the default Jekyll site. In summary, it provides a configurable integration with the above features and services. It also uses the popular (mobile friendly!) Twitter Bootstrap as the theme, and supports the ability to easily change to another theme. Unfortunately this framework is no longer being maintained - its author has written his own static HTML generator :-0. 

[Octopress](http://octopress.org/) is a *framework* built on top of Jekyll which addresses the limitations of the default Jekyll site. In particular Octopress has many [themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes). Some of the popular themes have been copied numerous times - for example [Greyshade](https://github.com/shashankmehta/greyshade/wiki/Sites-using-Greyshade).

One consideration of using Octopress is that it delivers some extra plugins to make it easier to render different types of content (for example, an *HTML5 Video Tag* to make it easy to post mp4 HTML5 video with flash player fallback). A downside of depending on these plugins is that they cannot be used by the "safe mode" on Github pages - so to use this framework you must separately upload the source and output to Github.

* [Octopress documentation](http://octopress.org/)
 * [Overriding Styles](http://octopress.org/docs/theme/styles/)
* [Blogging with Octopress](http://mattgemmell.com/blogging-with-octopress/) (Matt Gemmell)
* [3rd Party Octopress Themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)
* [Octopress Themes](http://octopressthemes.com/) - octopressthemes.com


Of course there are lots of other sites and articles to learn from (or copy). A last few useful links I found are:

* [Fast mobile friendly website with jekyll](http://nicolashery.com/fast-mobile-friendly-website-with-jekyll)
* [Building static sites with Jekyll](http://code.tutsplus.com/articles/building-static-sites-with-jekyll--net-22211)
* [Sites using Jekyll](http://jekyllrb.com/docs/sites/)
* [jekyllthemes.org](http://jekyllthemes.org/)
* [jekyllthemes.net](https://www.jekyllthemes.net/)



# Summary

Jekyll makes a pretty basic blogging system out of the box, with the addition of other desirable features being easy but time consuming. Users who just want to get started blogging should consider avoiding the default Jekyll example, and instead copy and existing blog with the desired features, or use a *framework* like [Octopress](http://octopress.org/) which provides a more complete and configurable blogging site. 

I could have saved myself a lot of time by using Octopress or copying a more complete site rather than starting with the default project (before I moved to Poole). No regrets - I learned a lot and had some fun.





