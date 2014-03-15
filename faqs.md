---
layout: page
title: "FAQs"
description: ""
---
{% include JB/setup %}



##Notes##
The `$` sign refers to entries in terminal, while `:` refers to entries in Vim.

##Linux (Mint Debian)##

**Q**. What is the keyboard shortcut for the *Run application* dialog?

A. Alt + F2

##Vim##

**Q**. What file type does Vim think is open in the buffer?

A. In the buffer run `:set filetype?`.

**Q**. How to set a color scheme foo (for highlighting) in the current 
buffer?

A. In the buffer run `:colorscheme foo`.

**Q**. What color scheme is Vim using for the current buffer?

A. In the buffer run `:colorscheme`.

**Q**. How many colors does my terminal support?

A. Download the _colortest_ script from [www.vim.org](http://www.vim.org/scripts/script.php?script_id=1349),
open a terminal wherever you saved it and run `$ perl colortest -w`, to see 
available colors displayed in your terminal.

**Q**. How to set the file in the current buffer as type foo (for highlighting, 
for example)?

A. In the buffer run `:set filetype=foo`.

**Q**. How to set and use spell-check (starting Vim 7)?

A. In the buffer run `:set spell spelllang=en_us` to affect all buffers and
`:setlocal spell spelllang=en_us` to affect only the current buffer.
To deactivate run `:set nospell`. Use `]s` and `[s` to move to next and 
previous misspelled words, respectively. Type `z=` with the cursor on a
misspelled word to get a list of possible replacements.

**Q**. How to compare two text files side-by-side?

A. Open the two files with a vertical split, place the cursor at the very
top of each buffer, and run `:diffthis` in each buffer. This mode can be
switched off running `:diffoff`.

Source: [Stack Exchange](http://unix.stackexchange.com/questions/1386/comparing-two-files-in-vim)


##Jekyll/Blog##

_Rake_ tasks assume you are using the rakefile from [github.com/refp16](https://github.com/refp16/refp16.github.com/blob/master/Rakefile) and that you have
installed the **github-pages gem** as instructed here: [https://help.github.com](https://help.github.com/articles/using-jekyll-with-pages). The rakefile is 
mostly from the Jekyll-Bootstrap project but I have adapted
some tasks found in [https://github.com/gummesson/jekyll-rake-boilerplate]().

**Q**. How to create new post titled foo?

A. In root directory of site (USER.github.com) run `$ rake post title="foo"`.
The post is created in the `_posts` directory.

**Q**. How to create new page titled foo?

A. In root directory of site (USER.github.com) run `$ rake page title="foo"`.

**Q**. How to create a new draft (of post) titled foo?

A. In root directory of site (USER.github.com) run `$ rake draft title="foo"`.
The draft is created in the `_drafts` directory.

**Q**. How to move a _draft_ to the `_posts` directory (un-draft)?

A. In root directory of site (USER.github.com) run `$ rake publish` and 
choose the draft to be moved.

**Q**. How to locally build the site?

A. run `$ rake build`

**Q**. How to locally build, serve and watch the site (including drafts)?

A. run `$ rake watch["drafts"]`

**Q**. How to deploy your site to GitHub?

A. run `$ rake deploy["your commit message"]`

**Q**. How to remove a file from GitHub repository (and local system)?

A.

{% highlight bash %}
$ git rm foo
$ git commit -m "delete foo"
$ git push -u origin master
{% endhighlight %}

**Q**. How to remove a directory (with files) from GitHub repository (and
local system)?

A.

{% highlight bash %}
$ git rm -r some-directory
$ git commit -m "Remove some directory"
$ git push -u origin master
{% endhighlight %}

If that doesn't work remove the directory using standard a file browser or
terminal and then run:

{% highlight bash %}
$ git add -A
$ git commit -m "Remove duplicated directory"
$ git push -u origin master
{% endhighlight %}

Source: [Stack Overflow](http://stackoverflow.com/questions/6313126/how-to-remove-a-directory-in-my-github-repository)

##Other##

**Q**. Where does Okular save information on annotated pdfs?

A. `~/.kde/share/apps/okular`
