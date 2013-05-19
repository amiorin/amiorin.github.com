---
layout: post
title: "Cross platform vim script development"
date: 2013-05-19 10:01
comments: true
categories: [vim, windows]
---
I developed [vim-project][0] on my Mac and I wanted to be sure that it worked
also on Windows. It took me 1 day of work

Buy windows 8
Install windows 8
http://www.howtogeek.com/124286/how-to-uninstall-your-windows-product-key-before-you-sell-your-pc/
http://answers.microsoft.com/en-us/windows/forum/windows_8-windows_install/this-key-didnt-work-please-check-it-and-try-again/ba90b43b-682a-4633-9260-2d25c1f13903?page=2
```
HKLM/Software/Microsoft/Windows/CurrentVersion/Setup/OOBE
slmgr /rearm
```
download git
option: Run Git from the Windows Command Prompt

setup curl
https://gist.github.com/gmarik/912993/raw/2753fc4ad996d00bbe09f7af9faceb8e98433722/curl.cmd

ftp://ftp.vim.org/pub/vim/pc/gvim73_46.exe

##share
http://stackoverflow.com/questions/182750/map-a-network-drive-to-be-used-by-a-service
net use z:  \\VBOXSVR\gvim /persistent:yes

mklink _vimrc z:\_vimrc
mklink /D vimfiles z:\vimfiles
mklink /D .vim vimfiles

install font and powerline
http://codejury.com/consolas-font-in-vim-powerline-windows/

