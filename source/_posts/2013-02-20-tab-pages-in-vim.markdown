---
layout: post
title: "Tab Pages in Vim"
date: 2013-02-20 20:27
comments: true
categories: [vim]
---
This tip works only with MacVim (or GVim).

In Vim you can use one tab page per file, like in other editors, but I
think it doesn't work very well. I prefer to use one tab page for every
project. I used to use a MacVim window for project, but the copy and paste was
a nightmare.

{% img /images/dotfiles.png 250 %}
{% img /images/octopress.png 250 %}
{% img /images/gollum.png 250 %}

The rule is simple. Every **tab page** is a **project** and it has a **[local] working
directory** that is displayed in the ``guitablabel``.

## The code

```vim
" IMPORTANT! Inside your .gvimrc
augroup cwd
  au!
  au CursorMoved,WinEnter * call settabvar(tabpagenr(),'cwd', substitute(getcwd(), $HOME, '~', ''))
augroup END
set guitablabel=%{gettabvar(v:lnum,'cwd')}
set showtabline=1
```

## Event DirEnter and DirLeave

I would like to see in the next versions of Vim these two events. They would
be very useful to write new plugins *project-oriented*. In the meanwhile I've
downloaded the source code of Vim. After ten years, maybe I'll try again to
write some C code again.

For more info ``:h autocommand-events`` and ``:h tabpages``.


