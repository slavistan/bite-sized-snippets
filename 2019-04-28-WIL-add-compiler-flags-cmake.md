---
layout: what-ive-learned
title: Add compiler flags for all targets in CMake
tags: cmake
is_wil_snippet: true
---
**tl;dr** Call `add_compile_options()` *before* defining the project's targets.

```cmake
cmake_minimum_required(VERSION 3.12)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}")

project(c3srmatrix VERSION 0.0.1 LANGUAGES CXX)

# First add compile options...
add_compile_options( -fmax-errors=5 )

# and only later define the project's targets.
add_subdirectory(src)
```
