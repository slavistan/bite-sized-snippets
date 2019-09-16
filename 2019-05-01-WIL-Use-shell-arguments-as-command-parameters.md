---
layout: what-ive-learned
title: Use shell script arguments as parameters to commands
tags: gnu linux
is_wil_snippet: true
---
**tl;dr** Construct a literal command string and execute it using `eval`.

Some shell commands cannot be fed user input directly. Construct a command string and execute it using `eval`.

```sh
# Print a variable number of tildes. printf '~%.0s' {1..$1} does not work.
cmd='printf '"'"'~%.0s'"'"' {1..'$1'}'
eval $cmd
```
