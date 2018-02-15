---
title: Vim
date: 2017-12-24T08:56:05
tags: [ public ]
guid: b34f520d-f021-4811-82d9-fbcf6c187a54
---


<!--more-->

## Ex Ranges

 * [source](https://twitter.com/ed1conf/status/945033273125851136?s=09)
 * place cursor on line 4
 * `:1,+1p` (line 1 through line 5)
 * `:1;+2p` (line 1 through line 2, note that this *moves the cursor*)

## `'clipboard`

 * `:set clipbboard=unnamedplus` to make default yank etc go to `"+`
 * Handy when doing lots of migrating from one doc to another

## `"0` / `"1` / `"_`

 * `"0` is populated by yank, not delete.
 * `"1` is populated by change or delete *unless* a register is specified.
 * `"_` can be used to disable the population of any register.

## Regex Tricks

 * `\V` ~~ `grep -F`
 * `%(` ~~ perl's `(?:`
 * `\zs` / `\ze` controls match
   * `s/foo \zsbar\ze baz/biff/` replaces `foo bar baz` with `foo biff baz`

## `q:` / `q/`

  * [relevant blog post](https://blog.afoolishmanifesto.com/posts/editing-registers-in-vim-regedit/#do-you-hate-command-line-mode)
  * edit search or command history in command window
  * press `<C-f>` to upgrade to this
  * press `<Enter>` to exit

## `:t` / `:m`

 * Allows "remote" copying (ie no moving cursor)
 * Examples:
 * `:t .` == `yyp`
 * `:1t 2` == copy line one to line 3 (or to the end of line 2)
 * `:m` does the same thing, except moves instead of copies

## `:g` / `:vg`

 * Runs an ex command for each match
 * `:g/\v^\s*#/delete`
 * `:vg` inverts the match (like `grep -v`)


## `:makeprg` / `'errorformat`

 * Investigate using these for *more automation*
