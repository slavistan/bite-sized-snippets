---
layout: what-ive-learned
title: Create custom make targets using CMake
tags: cmake
is_wil_snippet: true
---
**tl;dr** `add_custom_target(foo command)` will execute the command when `make foo` is run.

This can be used to integrate external tools into the CMake project such as static analysis checkers. The following example will run the cppcheck analysis tool when `make cppcheck` is run.

```cmake
add_custom_target(cppcheck cppcheck --enable="warning,style,performance,portability" --template=gcc --project=compile_commands.json)
```
