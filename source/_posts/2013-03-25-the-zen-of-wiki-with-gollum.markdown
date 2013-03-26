---
layout: post
title: "The Zen of Wiki with Gollum"
date: 2013-03-25 13:47
comments: true
categories: [wiki, github, gollum]
---
I've always loved wikis. They are very useful for bookmarks and snippets.
After many years of [Dokuwiki][1], I switched to [Evernote][2]. The Evernote
experience was very disappointing. But the Dokuwiki solution is based on
Lamp that is so old and I didn't want to go back.

So I switched to [Gollum][3] and now I'm very satified.

* I can use Vim to edit my wiki.
* I can use Ack to search in my wiki.
* I can edit it on Github, if I need to.

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
" instant preview of markdown
Bundle 'suan/vim-instant-markdown'
" follow internal links of the wiki
Bundle 'mmai/wikilink'
```

## Sync
It's very boring to do every time you modify your wiki:

```sh
git pull
git add -A
git commit -m "minor changes"
git push
```

But if you use [Rvm][6], you can create a .rvmrc in the root of your wiki:

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
[2]: https://evernote.com/
[3]: https://github.com/gollum/gollum
[4]: http://www.nomachetejuggling.com/2012/05/15/personal-wiki-using-github-and-gollum-on-os-x/
[5]: https://github.com/kennethreitz/autoenv
[6]: https://rvm.io/
[7]: https://github.com/gmarik/vundle
[8]: http://jekyllrb.com

