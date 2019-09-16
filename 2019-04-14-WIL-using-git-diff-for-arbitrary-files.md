---
layout: what-ive-learned
title: Using git diff to compare arbitrary files
tags: git
is_wil_snippet: true
---
**tl;dr** Use `git diff --no-index` to compare two arbitrary files.

To use `git diff` as a regular diff tool the switch the no-index flag must be used. Otherwise, git will the filenames as multiple arguments to the same `git diff` call.

```sh
git diff --no-index file.a file.b
```
