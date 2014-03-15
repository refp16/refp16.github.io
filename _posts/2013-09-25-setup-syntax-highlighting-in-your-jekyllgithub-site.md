---
layout: post
title: "Setup syntax highlighting in your Jekyll/GitHub site"
description: ""
category: 
tags: [jekyll, tutorial, syntax highlighting, github, blog, site, pygments]
---
{% include JB/setup %}

I assume you have setup your site [using Jekyll-Bootstrap](http://refp16.github.io/2013/09/23/make-a-siteblog-using-jekyll-and-github).

Throughout, I refer to 
`~/USER.github.com/_includes/themes/twitter/default.html` as the 
_template-file_ and 
to `~/USER.github.com/_config.yaml` as the _config-file_.

Also, `$` and `>>>` are terminal prompts and refer to code submitted to 
Bash and Python terminals. That, you don't type in your terminal.

###1. Get necessary packages###
Install [python-pygments](http://pygments.org/) in your system. This is the 
package in charge of the coloring.

###2. Create your stylesheet###
The stylesheet does what its name suggests: it provides style/formatting for
your source code. If you're curious, go ahead and open it with your favorite
text editor.

Open a terminal window, change to the root of your site directory and create a 
stylesheet for your template-file using Pygments CSS classes:

{% highlight bash %}
$ cd ~/USER.github.com
$ pygmentize -S default -f html > pygments_style.css
{% endhighlight %}

This outputs the file `pygments_style.css` to your current directory. The 
stylesheet can be named (almost?) anything as long as you set it up 
accordingly in your template-file (see point -4-).
`default` is 
the _style_ name and this can be set to any style in
python-pygments. As noted in [http://pygments.org/docs/styles/]() you can
get a list of available styles running the following in a python session:

{% highlight python %}
>>> from pygments.styles import get_all_styles
>>> styles = list(get_all_styles())
>>> print styles
{% endhighlight %}

which outputs

{%highlight python%}
['monokai', 'manni', 'rrt', 'perldoc', 'borland', 'colorful', 'default', 'murphy', 'vs', 'trac', 'tango', 'fruity', 'autumn', 'bw', 'emacs', 'vim', 'pastie', 'friendly', 'native']
{% endhighlight %}

For a visual guide see 
[http://blog.favrik.com](http://blog.favrik.com/2011/02/22/preview-all-pygments-styles-for-your-code-highlighting-needs/#stylesheetNavigator).

###3. Adjust your site configuration file###
Introduce `pygments: true` in your config-file.

###4. Adjust your HTML template file###
Introduce the following in the `<head>` section of your template-file:

{% highlight css %}
<link rel="stylesheet" href="/pygments_style.css">
{% endhighlight %}

###Usage###
Now you can highlight source code inserting in your your markdown posts/pages 
something like the following:

    {{ "{% highlight language "}}%}  
	   your code goes here  
	{{ "{% endhighlight "}}%}

Substitute out _language_ with any of the languages supported by 
python-pygments (see [http://pygments.org/languages/]()).

###See also###
[http://pygments.org/]()

[http://pygments.org/docs/quickstart/#command-line-usage]()

###Credits###
[http://truongtx.me/2012/12/28/jekyll-bootstrap-syntax-highlighting/]()


