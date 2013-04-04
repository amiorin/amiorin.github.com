---
layout: post
title: "The Zen of Wiki with Gollum"
date: 2013-03-25 13:47
comments: true
categories: [wiki, github, gollum, vim]
---
I've always loved wikis. They are very useful for bookmarks and snippets.
After many years of [Dokuwiki][1], I switched to [Gollum][3] for these
reasons:

* I can use Vim to edit my wiki pages.
* I can use Ack for searching.
* I can read/edit it on Github, when I'm not on my MacBook.

## Setup
Create a repository in Github (I use the repository of my blog). Click ``wiki``
→ ``Git Access``.  Clone the wiki and you are done.

## Edit
If you want to edit your wiki in Chrome with Gollum, read this [article][4]. If
you prefer to use Vim, I suggest you to install these plugins with [Vundle][7]:

```vim
" open links in chrome
Bundle 'tyru/open-browser.vim'
" syntax highlight
Bundle 'tpope/vim-markdown'
" follow internal links of the wiki
Bundle 'mmai/wikilink'
```

## Reloadlive
If you want to see the wiki page rendered in your browser while you are
writing it, I have written a gem called [Reloadlive][9].

```bash
$ gem install reloadlive
# inside the directory of gollum
$ reloadlive
```

![Reloadlive demo](https://raw.github.com/amiorin/reloadlive/master/demo.gif)

## Sync
It's very boring to do every time you modify your wiki:

```sh
git pull
git add -A
git commit -m "minor changes"
git push
```

But if you use [Rvm][6], you can create a ``.rvmrc`` in the root of your wiki:

```sh
# .rvmrc
git pull && git add -A && git commit -m "minor changes" && git push
```

Every time you cd, Rvm looks for a file called .rvmrc. If it finds it, it
executes it. If you don't use Rvm, you can use [Autoenv][5].

```sh
# alias to sync when you are already in the root of the wiki.
alias gsync="sh ./.rvmrc"
```

## Conclusion

* No database.
* Password protected if you need.
* Distribuited.
* Autosync.
* It works offline.
* Vim editing instead of the ``textarea``.
* Regex search with Ack.
* Instant preview in the browser.
* Markdown language like in [Jekyll][8].

I'm ok for the next 10 years. :-)

[1]: https://www.dokuwiki.org/dokuwiki
[3]: https://github.com/gollum/gollum
[4]: http://www.nomachetejuggling.com/2012/05/15/personal-wiki-using-github-and-gollum-on-os-x/
[5]: https://github.com/kennethreitz/autoenv
[6]: https://rvm.io/
[7]: https://github.com/gmarik/vundle
[8]: http://jekyllrb.com
[9]: https://github.com/amiorin/reloadlive

