---
title: Leatherman
date: 2018-01-08T21:53:22
tags: [ public, project, oss ]
guid: 6334f6bf-3927-416d-af7c-579cb5248449
---


<!--more-->

[Leatherman](https://github.com/frioux/leatherman) is a project to migrate
scripts from [my dotfiles](https://github.com/frioux/dotfiles) to golang.  The
first candidates are scripts written in Perl or Python that have non-core deps,
as those tend to be a hassle.  On the other hand they seem to be the least used.

Any standalone go things I use should be migrated to this framework (for example
weird AWS things that I optimize in go.)

## Next Steps

 * Convert backlight
 * Convert bible-handler
 * Convert email-fix-in-reply-to
 * Convert expand-url
 * Convert export-bamboohr
 * Convert export-bamboohr-tree
 * Convert fn
 * Convert gen-pass
 * Convert graph-by-date
 * Convert group-by-date
 * Convert mail-picture
 * Convert minotaur
 * Convert pomotimer
 * Convert prepend-emoji-hist
 * Convert replace-unzip
 * Convert rss
 * Convert store-hist
 * Convert yaml2json
 * Refactor addrs
    * remove channel
    * use contact{addr, name string, score float64} type
 * Refactor ec2-resource-for-ip
    * Add docs
    * Use new AWS SDK
