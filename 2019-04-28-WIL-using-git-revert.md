---
layout: what-ive-learned
title: Using git revert to get back to working code
tags: git
is_wil_snippet: true
---
**tl;dr** Find a working commit using `git checkout master~N` and revert back with `git revert --no-commit master~N..master`.

Git revert is used to undo the changes introduced by single commits *by way of modifying the existing files* (nothing in the git tree is deleted). The arguments passed to `git revert` identify one or more commits.

In order to revert to the state of a certain commit, e.g. `master~4` every commit along the way must be reverted. This is done using `git revert --no-commit master~4..master`. The `--no-commit` flags prevents git from automatically creating commits from the changed files.
