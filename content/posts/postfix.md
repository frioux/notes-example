---
title: Postfix
date: 2017-12-24T05:40:01
tags: [ public ]
guid: c19b7eaa-991b-4b69-8555-d5830410d31c
---


<!--more-->

 * List queue: `postqueue -p` / `postqueue -j`
 * Show email: `postcat -vq $id`
 * Flush Queue: `postqueue -f`
 * Delete email from queue: `sudo postsuper -d $id`
