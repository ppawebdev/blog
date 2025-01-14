---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Cloud", "AWS", "Sceptre" ]
date: 2019-11-21
draft: false
lastmod: 2019-11-21
tags: [ "programming", "cloud", "AWS", "Sceptre" ]
title: "Sceptre"
type: "page"
---

## Overview

_Sceptre_ is a 3rd party open-source tool by Cloudreach to drive AWS CloudFormation. It provides a layer of abstraction over CloudFormation to make created and maintaining cloud infrastructure easier.

GitHub Repo: https://github.com/Sceptre/sceptre

## Installation

Sceptre can be installed with Python:

```bash
$ pip install sceptre
```

## Stacks

Each _Stack_ in Sceptre is organized by one or more _Stack Groups_.

```bash
$ sceptre create <stack_name>
```

```bash
$ sceptre delete <stack_name>
```
