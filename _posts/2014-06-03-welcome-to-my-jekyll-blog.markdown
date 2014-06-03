---
layout: post
title:  "Welcome to my Jekyll blog"
date:   2014-06-03 20:44:31
tags:
- jekyll
---


Welcome to my brand-spanking-new [Jekyll-powered](http://jekyllrb.com/) blog, hosted for *free* on [Github pages](https://pages.github.com/). After years of blogging on company blogs, I've decided it is time I had my own place to talk more generally about communities, writing, and anything else that interests me. 

The main reason I've considered Jekyll for the blog (rather than WordPress), is that it will be used for the documentation platform in an upcoming technical writing job. Creating a blog has been a very good way to get up and running quickly! It has also been a good way to get familiar with [Liquid](http://docs.shopify.com/themes/liquid-basics), and to refresh my CSS and JavaScript. 

For those that are interested, this post provides a brief overview of Jekyll, my blog, and other Jekyll-based blogging frameworks. 

<img alt="Jekyll official logo" src="http://jekyllrb.com/img/logo-2x.png" />

# What is Jekyll?
[Jekyll](http://jekyllrb.com/) is an open-source static HTML generator tool which builds static HTML pages from plain text files written in wiki syntax ([Markdown](http://daringfireball.net/projects/markdown/) or [Textile](http://textile.sitemonks.com/)). The content, structure and appearance of the site can be controlled using the [Liquid](http://docs.shopify.com/themes/liquid-basics) templating language, along with HTML and CSS. The tool also has support for various types of plugins, which can further customise the behaviour and output of the generated content.

While Jekyll can be used for generating any sort of HTML site, it does have features specifically to support blogging, and comes with an "vanilla" blog project.


# Why a Jekyll blog?

Common reasons given by bloggers for using Jekyll are listed below:

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

# Brief overview of the options


## Default Jekyll

This is the approach I used! 

The [Jekyll QuickStart](http://jekyllrb.com/docs/quickstart/) shows how to create your own default blog using the 'Jekyll new' command and start a local server to browse it. 
The main problem with this default blog is that it is missing many of the features you would commonly expect: *social widgets*, *tags*, *search*, *analytics*, and most importantly, the ability to add *comments*. While the CSS does have basic support for mobile layouts, and is simple enough to understand, this is not a particularly inspiring theme.

In my opinion you can choose not to enable comments (though these are possibly the [easiest feature to add](http://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions)) but social plugins are a necessity. Adding all the features took me much longer to set up than [the single day suggested in this article](http://erjjones.github.io/blog/How-I-built-my-blog-in-one-day/), mostly because I spent so long modifying the CSS to get additional features to lay out the way I wanted.

 The Internet has many articles and examples (which you can copy) showing how to extend the basic blog to add the above features. Here are a few I found particularly useful:

* [Disqus - Jekyll installation instructions](http://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions)
* [Jekyll From Scratch - Extending Jekyll](http://pixelcog.com/blog/2013/jekyll-from-scratch-extending-jekyll/)
* [How I built my blog in one day](http://erjjones.github.io/blog/How-I-built-my-blog-in-one-day/)
* [How I Created a Beautiful and Minimal Blog Using Jekyll, Github Pages, and poole](http://joshualande.com/jekyll-github-pages-poole/)
* [Building static sites with Jekyll](http://code.tutsplus.com/articles/building-static-sites-with-jekyll--net-22211)
* [Sites using Jekyll](http://jekyllrb.com/docs/sites/)
* [jekyllthemes.org](http://jekyllthemes.org/)
* [jekyllthemes.net](https://www.jekyllthemes.net/)


## Octopress

[Octopress](http://octopress.org/) is a *framework* built on top of Jekyll which addresses the limitations of the default Jekyll site. In particular Octopress has many [themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes). Some of the popular themes have been copied numerous times - for example [Greyshade](https://github.com/shashankmehta/greyshade/wiki/Sites-using-Greyshade).

One consideration of using Octopress is that it delivers some extra plugins to make it easier to render different types of content (for example, an *HTML5 Video Tag* to make it easy to post mp4 HTML5 video with flash player fallback). A downside of depending on these plugins is that they cannot be used by the "safe mode" on Github pages - so to use this framework you must separately upload the source and output to Github.

* [Octopress documentation](http://octopress.org/)
 * [Overriding Styles](http://octopress.org/docs/theme/styles/)
* [Blogging with Octopress](http://mattgemmell.com/blogging-with-octopress/) (Matt Gemmell)
* [3rd Party Octopress Themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)
* [Octopress Themes](http://octopressthemes.com/) - octopressthemes.com

## Jekyll Bootstrap

The [Jekyll Bootstrap](http://jekyllbootstrap.com/) also addresses many of the problems of the default Jekyll site. In summary, it provides a configurable integration with the above features and services. It also uses the popular (mobile friendly!) Twitter Bootstrap as the theme, and supports the ability to easily change to another theme. 

Unfortunately this framework is no longer being maintained - its author has written his own static HTML generator :-0. 

# Summary

Jekyll makes a pretty basic blogging system out of the box, with the addition of other desirable features being easy but time consuming. Users who just want to get started blogging should consider avoiding the default Jekyll example, and instead copy and existing blog with the desired features, or use a *framework* like [Octopress](http://octopress.org/) which provides a more complete and configurable blogging site. 

I could have saved myself a lot of time by using Octopress or copying a more complete site. No regrets - I learned a lot and had some fun.




