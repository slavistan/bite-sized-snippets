---
layout: what-ive-learned
title: Integrate clang-tidy into your CMake project.
tags: cmake clang-tidy
is_wil_snippet: true
---
**tl;dr** Use `set(CMAKE_CXX_CLANG_TIDY "${CLANG_TIDY_EXECUTABLE}" "-checks=*")` to enable clang-tidy analysis for each target by default.

CMake provides integrates clang-tidy via the target property `CXX_CLANG_TIDY`. In order to express the intent to perform a clang-tidy analysis of a specific target the property has to be set accordingly:

```cmake
# ...

add_executable(my_executable my_source.cpp)
set_target_property(my_executable PROPERTIES
  CXX_CLANG_TIDY "{CLANG_TIDY_EXECUTABLE}" "-checks=*")
```

The `CXX_CLANG_TIDY` property is default-initialized to `CMAKE_CXX_CLANG_TIDY`. Thus, setting the default accordingly causes all targets to be analyzed by default.

```cmake
# Define CLANG_TIDY_EXECUTABLE
find_program(
  CLANG_TIDY_EXECUTABLE
  NAMES "clang-tidy"
  DOC "Path to the clang-tidy executable")

# If clang-tidy was found set the default property accordingly.
if(CLANG_TIDY_EXECUTABLE)
  message(STATUS "clang-tidy found at '${CLANG_TIDY_EXECUTABLE}'")
  set(CMAKE_CXX_CLANG_TIDY "${CLANG_TIDY_EXECUTABLE}" "-checks=*")
endif()
```
