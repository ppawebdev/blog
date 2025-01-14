---
authors: [ "Geoffrey Hunter" ]
date: 2019-01-04
draft: true
lastmod: 2019-01-04
tags: [ "YAML", "serialization", "configuration", "data", "file", "Javascript", "object notation" ]
title: "YAML"
type: "page"
---

## Overview

YAML, or **YAML Ain't Markup Language**, is a human-readable data serialization format. It is commonly used to store configuration data for software applications.

The official site can be found at [https://yaml.org/](https://yaml.org/) (which is written in YAML format!!!).

JSON is a valid subset of the YAML specification, which means a `.json` file is a valid YAML file, and you can embed JSON syntax inside a YAML file.

## A List

All members of a basic list start with `- ` (a hash and a space):

```yaml
colors:
    - red
    - green
    - blue
```

You can also specify a list in a much more condensed form:

```yaml
colors: ["red", "green", "blue"]
```

This terser syntax is called a _Flow collection_.

## A Collection (Dictionary)

All items in a dictionary take the form `key: value` (there must be a space after the colon):

```yaml
my_dict:
    date: 2019-01-01
    color: red
    location: north
```

## Comments

YAML comments begin with a `#` (hash symbol, or Octothorpe if you're feeling fancy).

```yaml
# This is a comment
```