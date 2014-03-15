---
layout: post
title: "Setting shared syntax stylesheets (CSS files) for various themes"
description: ""
category: 
tags: []
---
{% include JB/setup %}

After installing several Jekyll-Bootstrap themes for my site as indicated 
[here](http://jekyllbootstrap.com/usage/jekyll-theming.html), I wanted to 
have a centralized place where each theme's _template-file_ (i.e. the one
found here `~/USER.github.com/_includes/themes/some-theme/default.html`) 
could feed off the `css` stylesheet file used for code highlighting. What I
noted after installing some themes is that each one of them kept its 
stylesheet in its own `../assets/themes/some-theme/css` directory. Because [I 
use stylesheets created by Python Pygments](/blog/2013/setup-syntax-highlighting-in-your-jekyllgithub-site/), I want all the themes to have access to them
without copying a complete set of stylesheets in each theme directory.
In this way, for any theme in use, if I wanted to change the syntax 
highlighting, I would just make the appropriate modification in the `<head>` 
section of the theme's _template-file_. The modification consist only of
changing the name of the file used as stylesheet. For example, if I want 
to change from the `borland` stylesheet to the `autumn` one I would change
this

{% highlight html %}
    <link rel="stylesheet" href="{{ site.url }}/assets/syntax-pygments/syntax-pyg-borland.css" type="text/css" />
{% endhighlight %}

to this

{% highlight html %}
    <link rel="stylesheet" href="{{ site.url }}/assets/syntax-pygments/syntax-pyg-autumn.css" type="text/css" />
{% endhighlight %}

Before being able to do that, all that is necessary is to put all syntax 
stylesheets in a common directory in `../assets`, like `~/USER.github.com/assets/syntax-pygments`. The following is my simplified directory structure.
Note that for the `mark-reid` theme, I've left the syntax stylesheet 
provided with the theme in its original place (although this is not necessary).

<pre>
USER.github.com
|
|--assets
|	|
|	|-- syntax-pygments
|	|    |-- syntax-pyg-borland.css 
|	|    |-- syntax-pyg-autumn.css
|	|    +-- syntax-pyg-what-ever.css
|	|    
|	|
|	+-- themes
|	     |-- mark-reid
|            |        |----- css
|            |                |--- screen.css
|            |                +--- syntax.css
|            |          
|            |-- the-program
|            |        |----- css
|            |        |----- font
|            |        +----- skin
|            |
|            +-- twitter
|                     |----- bootstrap
|                     +----- css
|
+--OtherStuff
</pre>



