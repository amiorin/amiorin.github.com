---
layout: post
title: "A Vim plugin for editing fenced code blocks"
date: 2013-04-18 17:29
comments: true
categories: [vim, markdown]
---
## Introduction
[Fenced code blocks][4] are a very useful feature of GitHub Flavored Markdown.
With this plugin you can edit the fragment of code embedded inside the
markdown with the right filetype.

![Demo][5]

## Install
If you use [Vundle][1] you can install this plugin using Vim command `:BundleInstall amiorin/vim-fenced-code-blocks`.
Don't forget put a line `Bundle 'amiorin/vim-fenced-code-blocks'` in your `.vimrc`.

If you use [Pathogen][2], you just execute following:

```sh
cd ~/.vim/bundle
git clone https://github.com/amiorin/vim-fenced-code-blocks.git
```

If you don't use either plugin management system, copy the `plugin` directory to your `.vim` directory.

\*nix: $HOME/.vim
Windows: $HOME/vimfiles

## Use
This plugin defines 4 new commands:

* ``:E`` to edit in the same window, ``CTRL-^`` to go back to the markdown file
* ``:EV`` to edit in the vertical split window, ``CTRL-W l`` to go back to the markdown file
* ``:ES`` to edit in the horizontal split window, ``CTRL-W j`` to go back to the markdown file
* ``:ET`` to edit in a new tab.

All the commands accept the ``bang``.

## Self-Promotion
* Star the repository on [GitHub](https://github.com/amiorin/vim-fenced-code-blocks)
* Follow [amiorin](http://albertomiorin.com) on
  * [Twitter](http://twitter.com/amiorin)
  * [GitHub](https://github.com/amiorin)

[1]: https://github.com/gmarik/vundle.git
[2]: https://github.com/tpope/vim-pathogen
[3]: https://github.com/tpope/vim-rake
[4]: https://help.github.com/articles/github-flavored-markdown#fenced-code-blocks
[5]: https://raw.github.com/amiorin/vim-fenced-code-blocks/master/demo.gif
