---
layout: post
title: "Make a site/blog using Jekyll and GitHub"
description: ""
category: 
tags: [jekyll, jekyll-bootstrap, git, github, mathjax, blog, site]
---
{% include JB/setup %}


###0. Prerequisites###

I like installing packages using the official repositories using either 
Synaptic or `apt-get install foo`, even though this usually means not having
the latest version available. For this site, however, I ended up not doing
it for certain packages because it proved more convenient.

- Git (installed using Synaptic)
- Jekyll-Bootstrap framework (not a package, but a set of files _cloned_
from GitHub. More on this below)
- Rake (installed using Synaptic to easily execute some tasks related to
blogging, but not necessary)

###1. Setup a GitHub account###
Open an account an account with GutHub. Make sure to adjust your security 
settings so you are able to communicate with GitHub from your bash terminal.
This may involve setting a SSH passphrase. Check 
[https://help.github.com/categories/56/articles]() and more generally 
[https://help.github.com/]() for GitHub support.

###2. Create a GitHub repository for your site###
Create a repository named **USER.github.com**, where _USER_ is the user-name
of your GitHub account. When creating the repository, do not initiate it with
a README, .gitignore, or license file.

###3. Download the general framework for your site and publish###
These files provide the basics in order to easily start your blog/site.

Open a terminal window and go to the local directory that will contain your 
site directory (suppose it is the home folder). Run 

{% highlight bash %}
    $ git clone https://github.com/plusjade/jekyll-bootstrap.git USER.github.com
    $ cd USER.github.com
    $ git remote set-url origin git@github.com:USER/USER.github.com.git
    $ git push origin master
{% endhighlight %}

The first line clones the _Jekyll-Bootstrap_ project into the 
`~/USER.github.com` directory. The second line moves into that directory.
The third line sets a _remote_ so you can link the local directory to the
repository that was created earlier in the GitHub site. And finally, the
fourth line sends the content of your local directory to GitHub, and 
therefore, to the WWW. Notice
that _origin_ refers to the GitHub repository and _master_ to the name of
the Git branch in your local machine.

If all went well, you should be able to navigate to your new site
using your favorite web browser and pointing to http://USER.github.io.
(It can take a few minutes for your site to be served by GitHub).

###So, what's going on? Save yourself some trouble###
Basically, when you downloaded _Jekyll-Bootstrap_ you downloaded a suite
of _markdown_ and _html_ files arranged in such a way that when pushed to
your GitHub repository, GitHub parses them with a _Markdown_ interpreter and
Jekyll, and then does the publishing of the resulting HTML files.
This is the reason there's a lag between the moment you `git push` and 
when the site is available on the WWW. 

At times, GitHub can find an error in one of your Markdown/HTML files and 
won't be able to publish your latest modifications. If this is the case, 
you will receive an annoying email from GitHub indicating this was the case.

You can avoid this by doing a local build of your site directory. This just
means that you parse the files yourself in your machine and then preview
your site locally using a web browser, before sending the commit over to
GitHub. The local parsing of source files will indicate if there is any error
that must be wiped before pushing to GitHub. 
This preview is only available to you, and as such, also gives you some
liberty over the feel and look of your site before displaying it to the rest 
of the world.

To be able to do this, you need to install the **Jekyll** package.
One alternative is to use whatever version of Jekyll is available in oficial
repositories. I tried this and it worked for a while; until GitHub started
sending emails pointing to an error even though local builds of
the site were running just fine. This situation did not allow me to debug 
the source files as I was unable to detect what GitHub's parsing was 
complaining about.

Probably the best route to follow is installing the Ruby gem 'github-pages'.
This is a good idea because the gem provides the packages used by GitHub to
parse the files you send in. A successfull local build is likely to produce
a successfull GitHub build. To do this, you should install previously:

- Ruby (installed using Synaptic, both ruby1.9.1 and ruby1.9.1-dev)
- Bundle (installed using Synaptic)

Detailed instructions for the rest of the installation are at
[https://help.github.com/articles/using-jekyll-with-pages](). To build
the site locally, within the root of the site directory run 
`bundle exec jekyll serve`.

Now you can browse to http://localhost:4000 and see the site.Modify it as 
you find appropriate and check the changes locally. When you're happy with 
them, run `git push origin master` to deploy to the WWW.

###Make your first changes to the site###
As you have probably noticed already, the _Jekyll-Bootstrap_ project comes 
along with some sample pages and posts for your new site. The information
contained therein has basic instructions on how do modify the site to suit
your needs.

The first thing you should do is modify the `~/USER.github.com/_config.yml`
file to reflect your information. At this point, run `jekyll --server` and
check your site locally to visually aknowledge the changes you just 
made. 

Next, you can create new posts and pages using `rake post` and `rake page`,
respectively. Navigate to the root directory of your site:

    $ cd ~/USER.github.com

To create a new post titled _foo_, run

    $ rake post title="foo"

To create a new page titled _foo_, run

    $ rake page name="foo.md"

Both, posts and pages are created as markdown files which can be modified
with your favorite text editor. Posts are created in the 
`~/USER.github.com/_posts` directory. Pages can be created almost anywhere.
I have defined other rake tasks using code from 
[https://github.com/gummesson/jekyll-rake-boilerplate]() and adding it to
the original rakefile provided by the Jekyll-Bootstrap project. You can check
my rakefile at [https://github.com/refp16/](https://github.com/refp16/refp16.github.com/blob/master/Rakefile)

###Add the possibility of rendering mathematics###
If you're interested in using mathematics in your site, you can do so
using MathJax. I haven't found the ideal solution to this problem but
what I have will do for the moment.

Add the following JavaScript snippet to the `<head>` block of the HTML
template file `~/USER.github.com/_includes/themes/twitter/default.html`:

    <script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

With this minor change I have managed the following:

- One way of doing inline math: `\\( 1/x^2 \\)`, rendering \\( 1/x^{2} \\).

- Three ways of doing block math. 

The first one uses

    <div>$$ f = ma. $$</div>

The second one uses the LaTeX `equation` environemnt on its own:
    
    \begin{equation}
        \frac{1}{x^3}
    \end{equation}
    
and the third one uses surrounding `<div>` tags with the `equation` 
environment:
    
    <div>
    \begin{equation}
	\frac{1}{x^4}.
    \end{equation}
    </div>
    
These three pieces of code render, respectively: 
<div>$$ f = ma, $$</div>

\begin{equation}
    \frac{1}{x^3}
\end{equation}    


