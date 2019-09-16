---
layout: what-ive-learned
title: Generate a compilation database file using CMake
tags: cmake
is_wil_snippet: true
---
**tl;dr** `set(CMAKE_EXPORT_COMPILE_COMMANDS ON)` will generate a compilation database file called `compile_commands.json` inside the build directory.

A compilation data base lists the exact commands used to build every single source file.
