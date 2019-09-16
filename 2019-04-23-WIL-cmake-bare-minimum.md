---
layout: what-ive-learned
title: Bare-minimum C++ CMake project
tags: c++ cmake
is_wil_snippet: true
---
**tl;dr** Set up CMake using `cmake_minimum_required(VERSION 3.14)` and `set(CMAKE_CXX_STANDARD 20)`. Add executables afterwards.

A minimum C++ CMake project requires a minimum CMake version and the desired C++ standard to be specified.

```cmake
cmake_minimum_required(VERSION 3.12)
set(CMAKE_CXX_STANDARD 20)

# Now executables may be added to the project.
add_executable(test main.cpp)
```
