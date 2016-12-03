libpopcnt
=========
[![Build Status](https://travis-ci.org/kimwalisch/libpopcnt.svg)](https://travis-ci.org/kimwalisch/libpopcnt)
[![Build Status](https://ci.appveyor.com/api/projects/status/github/kimwalisch/libpopcnt?branch=master&svg=true)](https://ci.appveyor.com/project/kimwalisch/libpopcnt)
[![GitHub license](https://img.shields.io/badge/license-BSD%202-blue.svg)](https://github.com/kimwalisch/libpopcnt/blob/master/LICENSE)

```libpopcnt.h``` is a header only C/C++ library for counting the
number of 1 bits (bit population count) in an array as quickly as
possible using specialized CPU instructions e.g. POPCNT, AVX2.
```libpopcnt.h``` has been tested successfully using the GCC,
Clang and MSVC compilers.

The algorithms used in ```libpopcnt.h``` are described in the paper
[Faster Population Counts using AVX2 Instructions](https://arxiv.org/abs/1611.07612)
by Daniel Lemire, Nathan Kurz and Wojciech Mula (23 Nov 2016).

C/C++ API
=========
```C++
#include "libpopcnt.h"

/// Count the number of 1 bits in the data array.
/// @param data  An array
/// @param size  Size of data in bytes
uint64_t popcnt(const void* data, uint64_t size);

/// Count the number of 1 bits in x.
uint64_t popcnt_u64(uint64_t x);
```

How to use it
=============
At compile time you need to specify if your compiler supports the
```POPCNT``` & ```AVX2``` instructions.

```bash
# How to compile on x86 & x86_64 CPUs
gcc -mpopcnt -DHAVE_POPCNT -mavx2 -DHAVE_AVX2 program.c

# How to compile using Microsoft Visual C++
cl /O2 /EHsc /D HAVE_POPCNT /arch:AVX2 /D HAVE_AVX2 program.cpp

# How to compile on IBM POWER8 CPUs
gcc -mpopcntd -DHAVE_POPCNT program.c
```
