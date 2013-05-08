---
layout: post
title: "Autoread and autowrite in Vim"
date: 2012-12-10 15:24
comments: true
categories: [vim]
---
## What
Don't save or reload your buffers. Vim can do that for you.

## How
From my [.vimrc][1]
```vim
" autoread and autowrite
augroup save
  au!
  au FocusLost * wall
augroup END
set nohidden
set nobackup
set noswapfile
set nowritebackup
set autoread
set autowrite
set autowriteall

" persistent-undo
set undodir=~/.vim/undo
set undofile
```

## Why
``:w<CR>`` and ``<D-s>`` take too much time. We should not be worried of data
loss, because we have Git and ``:h persistent-undo``.

Additionaly how many times it's happened to waste time in Chrome, reloading
the page n-times, because we had forgot to save in Vim?

Using ``nohidden``, ``autowrite`` and ``update`` we are sure that everything
is saved.

```sh
# don't forget to create the directory for the undo files
mkdir ~/.vim/undo
```

## You don't need the scratch plugin
You would like to try a VimL snippet, create a ``scratch.vim`` somewhere. Use
a global mark ``mS`` (S is scratch).

Now with ``'S`` you are in your scratch buffer.

Use [vim-eval][0] to evaluate (``<C-c``) the file, the region or the line.

## Other global marks that I use
* ``'V`` my .vimrc
* ``'T`` my todos
* ``'0`` last file edited

## But the undo is not user-friendly
Yes, you're right, try Losh's [gundo][2]

```vim
Bundle 'sjl/gundo.vim'
```

The command is ``GundoToggle``.

[0]: https://github.com/amiorin/vim-eval
[1]: https://github.com/amiorin/dotfiles/blob/master/vimrc
[2]: https://github.com/sjl/gundo.vim
