---
author: gbmhunter
categories: [ "Programming", "Version Control Systems" ]
date: 2015-01-12
draft: false
lastmod: 2015-01-12
tags: [ "programming", "version control systems", "VCS", "git", "large", "shallow copy" ]
title: Managing Large Repos
type: page
---

## Overview

The size of a repository can grow in two orthogonal directions:

1. The size of the history
2. The size of the current repo data

Obviously, if a shallow copy has not been performed, the size of the history is always equal or greater than the size of the current repo data (assuming no compression has taken place, and the repo has no uncommitted changes).

## Shallow Clones

Git allows a shallow copy, keeping only the latest n commits, with the command:

```sh    
$ git clone --depth n
```

Git version 1.9 improved the capabilities of shallow clones dramatically, giving them full push/pull support between the shallow copy repo and a repo with the entire history.

As of 2015-01, [Mercurial does not support this feature](/programming/version-control-systems/mercurial/managing-large-repos).