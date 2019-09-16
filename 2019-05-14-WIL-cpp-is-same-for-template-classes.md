---
layout: what-ive-learned
title: How to implement `std::is_same` for template classes
tags: cpp
is_wil_snippet: true
---
**tl;dr** Inherit from `std::false_type` by default but inherit from `std::true_type` for the specialization.

```c++
/*
 * is_eigen_sparsematrix
 */
template <
  typename
  >
  struct is_eigen_sparsematrix : std::false_type {};

template <
  typename Scalar,
  int Options,
  typename StorageIndex
    >
  struct is_eigen_sparsematrix <
    Eigen::SparseMatrix<Scalar, Options, StorageIndex>
      >
      : std::true_type {};
```
