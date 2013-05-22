---
layout: post
title: "Cross platform vim script development"
date: 2013-05-19 10:01
comments: true
categories: [vim, windows]
---
I've developed [vim-project][0] on my Mac and I wanted to be sure that it worked
on Windows too.
I bought a Windows 8 license some time ago for only 29,99 € to update my Acer
from Windows Vista.
I could try the plugin in my Acer, but I wanted to have something similar to a
[Vagrant][1] setup.
So I've created a VirtualBox for Windows 8, but I've encountered some obstacles.

## Uninstall windows 8
You can have only one installation of Windows 8. So I followed the
instructions to uninstall the Windows 8 license from my Acer from [How-To Geek](http://www.howtogeek.com/124286/how-to-uninstall-your-windows-product-key-before-you-sell-your-pc/)

It wasn't enough. I had to call Microsoft to activate Window 8.

## Windows 8 upgrade with an empty disk
If you install windows 8 on an empty partition, you cannot activate your
Windows 8. I have found how to fix the problem [in the Microsoft
forum](http://answers.microsoft.com/en-us/windows/forum/windows_8-windows_install/this-key-didnt-work-please-check-it-and-try-again/ba90b43b-682a-4633-9260-2d25c1f13903?page=2)

## Installation of Vim
I've installed [this version of
vim](ftp://ftp.vim.org/pub/vim/pc/gvim73_46.exe)

## Setup of vundle in Windows
I've followed the instructions from [Vundle for Windows][2] to setup Git and
Curl.

## Shared Folder with VirtualBox
This is the hard part. I wanted to be able to modify my plugin from MacVim and
then restart Gvim to test it.

To achive this, you need to configure a VirtualBox shared folder.
Then you need to setup a network unit in Windows. The problem is that the
network unit must be visible by all users, because the symbolic links are
created as Administrator while vim is started as normal user.

I've found the solution on [stackoverflow][3]:

For this **hack** you will need ``psexec`` [SysinternalsSuite][4] by Mark Russinovich:

1. Open an elevated cmd.exe prompt (Run as administrator). Press the ``right
   command``. Write ``cmd`` and then ``<C-S-CR>`` (``ctrl-shit-enter``).

2. Elevate again to root using PSExec.exe: Navigate to the folder containing
   SysinternalsSuite and execute the following command ``psexec -i -s
   cmd.exe`` you are now inside of a prompt that is ``nt authority\system``
   and you can prove this by typing ``whoami``. The ``-i`` is needed because
   drive mappings need to interact with the user

3. Create the persistent mapped drive as the SYSTEM account with the following
   command ``net use z:  \\VBOXSVR\gvim /persistent:yes``

Now you can create the links, but you have to do this **hack** everytime you
restart Windows.

## Creating symbolic links in NTFS
My Gvim setup is in ``/Users/amiorin/Code/gvim``, ``gvim`` from now on.
``gvim/_vimrc`` is a link to ``~/.vimrc``. ``vimfiles`` is not a link, but a
real directory, because I use [Vundle](https://github.com/gmarik/vundle).  But
``gvim/vimfiles/bundle/vim-project`` is a link to
``~/.vim/bundle/vim-project``. ``gvim`` is ``Z:`` in Windows 8.

Using an elevated cmd.exe (``<C-S-CR``)
```sh
cd %USERPROFILE%
mklink _vimrc z:\_vimrc
mklink /D vimfiles z:\vimfiles
# Vundle uses .vim also on Windows.
mklink /D .vim vimfiles
```
Inside Gvim
```vim
BundleInstall
```
Then I removed my plugin from ``vimfiles/bundle`` and I have created a link
from ``~/.vim/bundle/vim-project`` to be able to use the same code in MacVim
and Gvim.

## Powerline with Consolas font
Here you find a patched [consolas for powerline](http://codejury.com/consolas-font-in-vim-powerline-windows/)
```vim
set guifont=Consolas\ for\ Powerline\ FixedD:h12
```

{% img /images/gvim.png %}

## Conditional ``.vimrc``
Some configurations are specific to one manchine. I've used the function
``hostname()`` in this way.

```vim
if hostname() ==# 'air.local'
  set guifont=Menlo\ for\ Powerline:h12
elseif hostname() ==# 'TOSHIBA'
  set guifont=Consolas\ for\ Powerline\ FixedD:h12
endif
```

``air.local`` is the Mac and ``TOSHIBA`` is the Windows 8.

## Conclusion
With this setup I can write my plugins in MacVim and test them on Gvim and
MacVim at the same time without any copy and paste of files or any commit and
pull. I could use Gvim, but I use a lot of shortcuts starting with the ``left
command`` in MacVim and the ``left command`` used by VirtualBox is a dead key
inside the guest os.

[0]: https://github.com/amiorin/vim-project
[1]: http://www.vagrantup.com/
[2]: https://github.com/gmarik/vundle/wiki/Vundle-for-Windows
[3]: http://stackoverflow.com/a/4763324/2268638
[4]: http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx
