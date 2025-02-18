---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Programming Languages" ]
date: 2018-06-26
description: "A tutorial on Python debugging, including how to use pdb."
draft: false
lastmod: 2019-06-12
tags: [ "programming", "programming languages", "Python", "pyrasite", "pdb", "escaping" ]
title: "Python Debugging"
type: "page"
---

## pdb

Keyboard Shortcuts

```text
n   step to Next line or current function returns   
c   continue until breakpoint is hit
b <line_num> set breakpoint at line number in current file
cl    clear all breakpoints (asks for confirmation)
```

### Escaping Variables Which Conflict With PDB Commands

Sometimes, you will run to run Python commands through the PDB console which will clash with PDB's own command set. One example would be if you had a variable called c, and wanted to assign to it:

```python
# (in a PDB debugging console)
c = 23
```

Instead of assigning the variable `c` the value `23`, PDB will interpret the above `c` as it's continue command. To prevent this from happening, prefix the command with `!`:

```python
!c = 23
```

## Entering A Running Python Process

[pyrasite-shell](http://pyrasite.readthedocs.io/en/latest/index.html) is a great tool for attaching to a running Python process. You can install it using `pip` with:

```sh    
$ pip install pyrasite
```

You can then attach a pyrasite shell to a running python process using the process ID (PID):

```sh    
$ pyrasite-shell 12345
```

You should then be presented with an interactive Python shell, and you can do things like print the stack trace for each thread:

```py    
import sys, traceback
for thread_id, frame in sys._current_frames().items():
    print(f'**** STACK TRACE FOR THREAD {thread_id} *****'
    traceback.print_stack(frame)
    print('***** END OF STACK TRACE *****')
```

Note that annoyingly, coping and pasting this code into the interactive console will not usually work (due to whitespace getting mangled perhaps?).

`pyrasite-shell` is a great tool for attaching to "hung" or "frozen" Python processes, which might be stuck in a loop or stuck in a blocked state waiting for something to happen.
