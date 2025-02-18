---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Programming Languages", "Python" ]
date: 2013-06-18
draft: false
lastmod: 2019-01-01
tags: [ "Python", "programming", "programming languages", "comments", "documentation", "docstrings" ]
title: "Comments And Documentation"
type: "page"
---

## Comments

Comments begin with a `#`.

```python
# This is a comment
```

[PEP 8](https://pep8.org/#maximum-line-length) recommends that comments should have a maximum line length of 72 characters. Comments longer than this should be split into multiple lines.

```python
# This is a really, really, really, really, really long comment that
# would exceed the maximum recommended comment line length of 72
# characters if it wasn't split into multiple lines.
```

## Docstrings

A docstring is an official way of in-place Python code documentation. It takes the form of blocks of text starting and ended with `"""` placed throughout the code.

```python
def my_func():
    """ This is a docstring """
```

When these comments are in the correct places, the Python bytecode compiler recognizes them and adds them to the `__doc__` parameter which can be inspected at runtime.

Python recognizes docstrings when the are placed at the start of functions, classes, modules (e.g. at the top of Python files and the directory also contains an `__init__.py`) and also when in the `__init__.py` file of a Python package.

A docstring is formally defined by [PEP 257](https://www.python.org/dev/peps/pep-0257/) as:

> A docstring is a string literal that occurs as the first statement in a module, function, class, or method definition. Such a docstring becomes the `__doc__` special attribute of that object.

Try to use `"""` for delimiting docstrings, and never `'''` (purely for consistency). If your docstrings need to contain backslashes you can use `r"""`, if you need to include unicode characters you can use `u"""`.

## Docstring Styles

There are a few popular docstring styled used. 

### reStructuredText

This is the official Python documentation style. It is feature rich, but not a simple as the Google style.

### Google Style

```python
def add(num1: int, num2: int) -> int:
    """
    Adds two numbers together.

    Args:
        num1 (int): The first operand.
        num2 (int): The second operand.

    Returns:
        int: The sum of the two operands.
    """

    return num1 + num2
```

`Args` can be replaced with `Parameters`.

### reStructured Text Style

The reStructured text style is used by [Sphinx](http://www.sphinx-doc.org/en/master/) to generate documentation (however Sphinx can also handle Google-style docstrings with the pre-packaged [Napoleon extension](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/)). It is the default docstrings style when using the JetBrains PyCharm IDE (although the IDE supports the other common styles also).

```python
def add(num1: int, num2: int) -> int:
    """
    Adds two numbers together.

    :param num1: The first operand.
    :type num1: int
    :param num2: The second operand.
    :type num2: int

    :returns: The sum of the two operands.
    :rtype: int
    """

    return num1 + num2
```

Notice how the type for each parameter has to be specified on it's own line with the `:type` and `rtype` identifiers, which is rather clunky!

### NumPy/SciPy Style

```python
def add(num1: int, num2: int) -> int:
    """
    Adds two numbers together.

    Parameters
    ----------
    num1 : int
        The first operand.
    num2 : int
        The second operand.

    Returns
    -------
    int
        The sum of the two operands.
    """

    return num1 + num2
```

## Docutils

[Docutils](http://docutils.sourceforge.net/) is a tool you can use to generate documentation from Python docstrings.