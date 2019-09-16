---
layout: what-ive-learned
title: "VIM One-Liner: Run opened script in different terminal"
tags: vim
is_wil_snippet: true
---

**tl;dr** `autocmd! BufWritePost * silent! !./myscript.zsh > /dev/pts/1`

