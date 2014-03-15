---
layout: post
title: "Backup your dotfiles with GitHub"
description: ""
category: 
tags: []
---
{% include JB/setup %}

The strategy used here is to keep the dotfiles in a special directory of
your choice and to _hardlink_ them to your home directory. We must hardlink
them because most applications will look for the files in the home directory.

###1. Make the special directory and move the original dotfiles###

The following example illusrates the process using a `.vimrc` file and a 
special directory named `~/dotfiles`.

{% highlight bash %}
$ mkdir ~/dotfiles
$ mv ~/.vimrc ~/dotfiles/vimrc
{% endhighlight %}

Note the file just moved does not have `.` as a prefix. This does not have
to be the case but in the next step we assume this is true. Recall that files
preceded with a dot are considered hidden files. Eliminating the 
prefix makes the files always visible in your file manager.

###2. Create the hardlinks###
The hardlinks are created using a bash script from 
[https://github.com/michaeljsmalley/dotfiles/](https://github.com/michaeljsmalley/dotfiles/blob/master/makesymlinks.sh). Download it and save it in 
`~/dotfiles`.

Open the script with a text editor and edit the _variables_ section so it
contains the appropriate directories in your system and the files that will
be hardlinked. On execution, 
the script creates symlinks for dotfiles in the home directory to your 
dotfile directory. The orginal dotfiles are also backed up.

###3. Git and GitHub###
Create a repository in GitHub (e.g. name it _dotfiles_) and then initiate a 
Git repository in your `~/dotfiles` directory. Then push the files to GitHub.
That's it.

###Credits###

[http://blog.smalleycreative.com/tutorials/using-git-and-github-to-manage-your-dotfiles/]()

