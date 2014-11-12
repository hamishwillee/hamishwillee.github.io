---
layout: post
title:  "Jekyll bootstrap documentation theme with multiple TOCs"
author: Hamish Willee
description: This post introduces a Jekyll theme (prototype) that is suitable for building sites with multiple TOCs defined in the site YAML source.
tags:
- jekyll
---


{{page.description}}

## Introduction

I've just created a (prototype) Jekyll documentation theme based on bootstrap. The theme allows you to define sidebar table of contents (TOC) and top navigation menu files in the site data (Yaml), and to assign them to pages based on the location of the page in the file system, the type of page, the collection, or in the page front-matter. 

This makes it possible to have separate but linked documentation sets within a single build (with independent TOC and look and feel). For example, you might build a single site with different navigation and appearance for documenting several different products for the same vendor.

<div class="alert alert-success" role="alert"><p>The theme is based on <a href="https://sendgrid.com/docs/index.html">SendGrid Docs</a>, a complete open source documentation theme for Jekyll which also includes the integration of analytics, SEO, search, and features to support "code items". SendGrid has a single TOC that it dynamically generates from the folder structure of the source documentation using a plugin.</p></div>

## What does it look like?

You can check out the [site here](http://hamishwillee.github.io/jekyll-bootstrap-docsite/), and the source is on [Github here](https://github.com/hamishwillee/jekyll-bootstrap-docsite). The image below is a screenshot from the site.

![Image  TOC](/images/blogs/20141112-jekyll-bootstrap-docs-breadcrumb.png)


## What can you do with the theme?

With this theme you can:

* Define TOCs and bootstrap navigation menus using nested YAML lists.
* Specify the TOC and menu files to use for pages in different folders, collection and types in the default front matter.
* Use a different name for TOC nodes than the doc title or folder title.
* Move documents in a TOC or menu hierarchy without changing their position in the file system. 
* Build the site using github's version of Jekyll (as it doesn't use plugins). 

In addition, the bootstrap theme used is based on bootstrap-sass, so you have access to all the bootstrap components, and can modify their appearance by changing variables in **main.scss**


## Alternatives

There are a lot of great static site generators (SSG). Two that are particularly popular:

* [Slate](https://github.com/tripit/slate) is popular in the API documentation field. 
  * It renders all markup files in a single output HTML file with a sidebar TOC. This has the benefit that no separate search is needed, because all documents are in the same output and the current context is maintained in the visible TOC. On the other hand, the page can be slow to load if it has many images. 
  * Slate also has a clever method of rendering code fragments in separate language-specific tabs alongside the related documentation.
* Sphinx is a very powerful SSG, which has a good understanding of code (particularly Python) and documents. It defines documents in restructured text. It is much more "mature" than Jekyll but only really "understands" document sets with a single TOC.

By comparison, Jekyll lets you do anything you like, with the cost that you have to create most of the functionality yourself. For the type of task described I might well use Jekyll. For web API documentation I would probably use Slate. For Python code I would definitely use Sphinx.
