---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Programming Languages", "Python" ]
date: 2018-01-17
draft: false
lastmod: 2018-01-17
tags: [ "programming", "programming languages", "Python" ]
title: Anaconda
type: page
---

## Overview

Anaconda exposes two important command-line tools, conda and source.

{{< figure src="/images/2018/02/anaconda-python-logo.png" width="598px" caption="The logo for Anaconda (Python distribution/environment)."  >}}

## How To Create And Use A Virtual Environment

This assumes you have installed anaconda and conda is available on your path.

First, create a new environment:

```sh    
$ conda create -n <your environment name>
```

Now activate this environment:

```sh    
$ source activate <your environment name>
```

Install your required packages:

```sh    
$ conda install -n <your environment name> <package>
```

{{% note %}}
If you don't specify an environment to install to (as above), Anaconda will install to the currently active environment. To install to any environment which is not currently active, add the option `-n <your environment name>` to the above command.
{{% /note %}}

Now you can run your python code!

When finished, you can deactivate your virtual environment with:

```sh    
$ source deactivate
```

## Listing All Local Environments

Use the following command to list all local environments:

```sh    
$ conda env list
```

The currently active environment will have an asterisk after it's name.

## Installing Non-Conda Packages

Non-conda packages can be installed into the current environment with other Python package managers such as pip:

```sh    
$ pip install <package name>
```

As long as a Anaconda environment is active, pip will install to the current environment only.
