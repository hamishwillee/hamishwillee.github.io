---
layout: post
title:  "Using Jekyll _includes as custom liquid functions"
author: Hamish Willee
description: This post shows how you can use files in the Jekyll **_includes** directory to implement function-like behaviour. 
tags:
- jekyll
---

{{ page.description}}

## Introduction


One of the frustrating limitations of [Liquid](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers) (Jekyll's templating language) is that there is no obvious way to declare your own functions. As a result, when you get started with Jekyll you may find yourself repeating blocks of template code, and even deciding that some actions are simply too complicated to safely implement without a plugin.

<div class="alert alert-success" role="alert"><p>This was the problem I had when implementing the table of contents (TOC) on my <a href="http://hamishwillee.github.io/jekyll-bootstrap-docsite/">Jekyll-bootstrap documentation theme</a>. Without functions, traversing a nested YAML list to create the TOC HTML would result in progressively complicated and unmaintainable code for every level of nesting required. </p></div>

What may not be obvious at first glance is that you can use Jekylls [includes](http://jekyllrb.com/docs/templates/#includes) as functions, passing in parameters and "returning" either text or variables for use in other functions. You can even include files recursively.


## How does it work?

### Creating the function

"Functions" are simply files, typically with the extension **.html**, in the site **_includes** directory (or a subdirectory of that folder). These can contain any HTML, markup, or [Liquid code](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers).

### Calling the function

You call the function to include the contents of the file using the ```include``` tag as shown:

{% highlight liquid %}
{% raw %}
{% include your_function.html %}
{% endraw %}
{% endhighlight %}


### Passing in parameters

If you need to pass in parameters you can do that too. The fragment below shows how you might pass in a string ```"a value"``` and a variable ```variable_name```.

{% highlight liquid %}
{% raw %}
{% include your_function.html some_parameter="a value" another_parameter=variable_name %}
{% endraw %}
{% endhighlight %}

Within the file you can access those parameters using ```{% raw %}{{ include.some_parameter }}{% endraw %}``` and ```{% raw %}{{ include.another_parameter }}{% endraw %}``` respectively.

<div class="alert alert-success" role="alert"><p>The parameters can be considered to be static const - they can't be changed within the function and you can't use them to return values.</p></div>

### Return values

The "return value" of the function is whatever text you output, i.e. a string. 

Sometimes you will want to further process the output of a function. In this case you can use the [Liquid capture tag](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers#variable-assignment) to assign the result of the function to a variable, and then run standard filters on it.

<div class="alert alert-success" role="alert"><p>You cannot return an "array" or any other variable than a string.</p> <p>If you need to do so, then convert the variable into some string format that you can then capture and reconvert into variable in the caller. </p></div>


## A real example

The [Jekyll-bootstrap documentation theme](http://hamishwillee.github.io/jekyll-bootstrap-docsite/) defines a table of contents using a YAML list with an arbitrarily deep nesting structure. Each level of the list can specify a ```url``` to a document or external site (with an optional ```name```) or a ```folder``` name, which contains other urls and/or folders.

A simple example of a structure with a nested folder is given below. 

{% highlight yaml %}
- folder: A folder
  contents:
   - url: /somepath/anydoc.html
   - url: /anypath/anotherdoc.html

   - folder: Nested Folder
     contents:
      - url: /anypath/anydoc1.html
      - url: /anypath/anydoc2.html


- folder: Another (peer) folder
  contents:
   - url: /anypath/anydoc3.html
     name: TOC defined name

- url: /anypath/anydoc4.html
{% endhighlight %} 

In order to open up the menu to the correct place when a page is loaded we need to mark its parent folder nodes as open in the HTML. Unfortunately this means that we need to iterate the structure twice: once to determine the breadcrumb of folders to the current article, and again to build the TOC using this information.

The function we use for the first iteration is [/_includes/functions/f_navtree_open.html](https://github.com/hamishwillee/jekyll-bootstrap-docsite/blob/gh-pages/_includes/functions/f_navtree_open.html). The function is initially called with the TOC for the whole menu as a parameter. 

{% highlight liquid %}
{% raw %}
<!-- Iterate all items at root level of the passed-in TOC -->
{% for navitem in include.theTOC %} 

  <!-- If item is a folder ... -->
  {% if navitem.folder %}

    <!-- Add its name to the list of folders and assign to iterfolders -->
    {% capture iterfolders %}{% if include.folders %}{{include.folders}},{% endif %}{{navitem.folder}}{% endcapture %} 

    <!-- Call function again with folder content, and iterfolders listing the folders above it -->  
    {% if navitem.contents %}
      {% include /functions/f_navtree_open.html theTOC=navitem.contents folders=iterfolders %} 
    {% endif %}

  <!-- If the item is an URL matching the current page, output the list of folders above it (passed in as include.folders) -->
  {% elsif navitem.url %}
    {% if page.url == navitem.url %}{{include.folders}}{% endif %} 
  {% endif %}

{% endfor %}
{% endraw %}
{% endhighlight %}

The function iterates through the items in the first level of the passed TOC (```include.theTOC```):

* If it encounters a folder, the function recursively calls itself to handle the next level of TOC. In this case the function is passed the TOC sub-tree and a comma separated list of all folders above the current point (```include.folders```).
* If it finds an URL that matches the current page, the function outputs the current value of ```{% raw %}{{include.folders}}{% endraw %}```. This is the "result" - a comma separated list of folders in the direct path above the current article.

The function is used in [/_includes/sidebar_tree.html](https://github.com/hamishwillee/jekyll-bootstrap-docsite/blob/gh-pages/_includes/sidebar_tree.html) as shown below:

{% highlight liquid %}
{% raw %}
{% capture openfolder_array %}{% include /functions/f_navtree_open.html theTOC=toc %}{% endcapture %}
{% assign openfolder_array = openfolder_array | strip_newlines | split: "," %}
{% include /functions/f_navtree.html theTOC=toc outer='true' opentree =openfolder_array %} 
{% endraw %}
{% endhighlight %}

First the function block is run within a ```capture``` block with the full TOC. The capture block assigns the returned comma separated list of folders (simply a string) to the ```openfolder_array``` variable. The variable is then stripped of newlines and split into an ```array``` object, and then ```assign```ed to the same variable name. Finally, the array is passed to the [/functions/f_navtree.html](https://github.com/hamishwillee/jekyll-bootstrap-docsite/blob/gh-pages/_includes/functions/f_navtree.html) where is is used to build the TOC.

## Tips

#### *Liquid* does not provide tags to allow you to dynamically build arrays. 

Use the [split](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers#standard-filters) function to split up a string to create an array. This approach is used above to turn the folder names list into an array/list so that it can be iterated.

#### Comments, space and newlines in functions are part of the output. 

Whatever code or comments, or even whitespace you put in a function will become part of the output HTML. Often this is fine, but if you want to further parse the content, this can result in unpredictable output. 

In functions where it matters omit all comments, left align all the rows, and remove spaces. You will still have line breaks, but these can be stripped using a filter.


#### strip_html just removes the tags

Stripping HTML removes the tags, but not the contained content. Unfortunately you can't use HTML stripping to remove comments before displaying your function output!

#### Parameters are "static const"

Parameters passed into a function (```include.param```) cannot be modified in the function. 


#### Scope is unclear - reset your temporaries

The scope of variables is a little unclear to me. I've found it "good practice" to reset temporary variables used in my functions before using them.



## Summary

Using *includes* as functions can allow you to perform quite complicated calculations in liquid, without having to resort to plugins. 

