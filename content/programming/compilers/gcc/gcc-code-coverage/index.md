---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Compilers", "GCC" ]
date: 2017-11-29
draft: false
lastmod: 2017-11-29
tags: [ "programming", "compilers", "GCC", "code coverage" ]
title: "GCC Code Coverage"
type: page
---

## Overview

GCC has built in functionality to generate code coverage data for libraries and executables you build with it. A number of other GNU tools are provided which can then read and display the generated coverage data

Coverage monitoring code can be inserted into your executable by providing gcc with the `-coverage` flag when compiling (which is shorthand for providing the the flags `-fprofile-arcs -ftest-coverage`):

```sh
$ gcc example.c -o example -coverage;
```

When running the compiled executable, `.gcda` files should be created for each source file.

`lcov` can be used to view the coverage data. lcov can be installed on Debian-like systems such as Ubuntu with:

```sh    
$ sudo apt install lcov
```

You can then "capture" the data with `lcov` using:

```sh
$ lcov --capture --directory <path> --output-file coverage.info
```

And then generate HTML files with:

```sh    
$ genhtml coverage.info --output-directory out
```

These visual HTML files are put into the `out/` directory and can be viewed in your browser.

## Troubleshooting

**undefined reference to `__gcov_merge_add`**

This is usually because the gcov library has not been linked with your library/executable. Usually this will happen automatically if you compile and link with the same gcc command. If compiling and linking separately (or using something like CMake), you may have to provide the linker flags `-coverage` and `-lgcov`.
