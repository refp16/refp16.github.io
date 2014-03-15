---
layout: post
title: "Installing and using color schemes in Vim"
description: ""
category: 
tags: [vim, syntax highlighting, color schemes, text editor] 
---
{% include JB/setup %}

Installing and making use of color schemes for syntax
highlighting in Vim is quite easy.

The first thing you may want to do is download some ready-made color
schemes available in the Web. Some nice options can be found here:
[www.vimninjas.com](http://www.vimninjas.com/2012/08/26/10-vim-color-schemes-you-need-to-own/) (unzip if necessary).

The next step is to save your color scheme files in 
the `~/.vim/colors` directory.
If you don't have it, you can just create it. The schemes should be available
for use now (or after a Vim restart, maybe). To use one within any Vim session,
execute `:colorscheme foo` where
`foo` is the the name of your color scheme file without the *.vim* extension.
For example if you just installed the **codeschool.vim** scheme, type 
`:colorscheme codeschool`. This will set the new scheme for the duration
of your current Vim session. To permanently set the scheme, modify your
`~/.vimrc` file to include `colorscheme codeschool` (create the **.vimrc** file
if you have none).
