---
layout: what-ive-learned
title: Integrate MS-GSL assertions into your CMake project
tags: cmake ms-gsl
is_wil_snippet: true
---
**tl;dr** Use `add_compile_definitions($<IF:$<CONFIG:Release>, ..., ...>)` to control the behaviour of assertions depending on your build type.

```cmake
# Add this to the root CMakeLists.txt to define `GSL_TERMINATE_ON_CONTRACT_VIOLATION` for the Debug build and to define `GSL_UNENFORCED_ON_CONTRACT_VIOLATION` for every other build type. This causes a violation of any pre- or post-condition to terminate the application in case of the Debug build and to ignore the violation for any other build type, minimizing the run-time cost.

add_compile_definitions($<IF:$<CONFIG:Debug>,GSL_TERMINATE_ON_CONTRACT_VIOLATION,GSL_UNENFORCED_ON_CONTRACT_VIOLATION>)
```
