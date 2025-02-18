---
authors: [ "Geoffrey Hunter" ]
date: 2013-05-28 01:51:22+00:00
draft: false
title: Makefiles
type: page
---

## Overview

Makefiles are a way of making a **"one touch" build solution for source code**. They are a type of file used by the GNU command **make**. They take multiple file inputs, do some part or all of the code build process, and produce output(s). They are commonly used to create executables, object files, or libraries (combined object files) from source code. They come in particularly useful when dealing with large projects.

They are textfiles that are stored with the filename "Makefile" (or "makefile"), with no file extension (**do not** call it makefile.txt!). The capital M version is recommended because it persists at the top of the directory, along with other important files like the README.

Makefiles are most commonly used to compile code for Linux environments, but also works in Windows, and for embedded systems.

Unlike most other programming/scripting languages, Makefiles are white-space sensitive. This can be annoying! Take care when coping makefile code from the internet, the clipboard can easily convert tabs into spaces and cause the makefile **code to break**.

Make can be then used by "higher-level" build programs, such as the [Autoconfig](http://www.gnu.org/savannah-checkouts/gnu/autoconf/manual/autoconf-2.69/html_node/index.html#Top) and [Automake](http://www.gnu.org/software/automake/) tools .

## The Simplest Possible Makefile

The simplest possible makefile is (please correct me if I'm wrong):

```make 
make: main.o
        gcc -o main.o main.c
```

If in Linux, opening a terminal, typing make and pressing enter while in the same directory as this makefile will compile a file called main.c with the GCC compiler and produce the output executable file `main.o`.

The primary three things a Makefile consists of are **targets**, **prerequisites**, and **recipes**. The above code contains two of these, `main.o`, which is the target, and `gcc -o main.o main.c`, which is the recipe. Make interprets this code as saying "You make main.o by running the command gcc -o main.o main.c in the terminal.". Note that all recipes are run in the terminal, and each new recipe (which is on a new line), is **run in a different instance of the terminal**.

{{% warning %}}
There is a tab infront of the recipe gcc .... . This is important! **All recipes must be proceeded by a tab.**
{{% warning %}}

If no parameters are passed in when you call make, the first rule in the makefile will be run.

## Adding Variables

Make supports variables that are defined before they are used in a rule. The value of the variable is substituted to replace the constant at run-time, similar to the C preprocessor.

You assign a value to a variable in the following ways:

<table>
    <tbody >
        <tr >
            
<td >
                VARIABLE = VALUE
            
</td>
            
<td >
                Normal assignment of a variable. Any other variables within in it are recursively expanded when the variable is used, not when it is declared. This is the same bahvaviour you would expect from a variable declared in C.
            
</td>
        </tr>
        <tr >
            
<td >
                VARIABLE := VALUE
            
</td>
            
<td >
                Any other variables within in it are expanded on declaration (instanlty). This is similar behaviour to if you declared a const variable in C++.
            
</td>
        </tr>
        <tr >
            
<td >
                VARIABLE ?= VALUE
            
</td>
            
<td >
                This sets the variable only if it doesn't have a value already. If the variable hasn't already been set, the actual calculation of the value will be deferred intil when it is used (like VARIBLE = VALUE.
            
</td>
        </tr>
        <tr >
            
<td >
                VARIABLE += VALUE
            
</td>
            
<td >
                This appends VALUE to the value that VARIBALE already has. Determining when to calculate the variable follows how it was initially set (i.e. with = or :=).
            
</td>
        </tr>
    </tbody>
</table>
    

There are common names that most people use for variables, which are shown below.

```text
CC
CFLAGS
```text

Using wildcards in variable assignment requires special syntax, see the Wildcards section.

## Wildcards

Wildcards are a great way to make automatic makefiles, i.e. makefiles that you do not need to continuously update as you create/delete code files.

One of the most common uses for a wildcard is with the "clean" rule, which is usually along the lines of:

```text
clean : 
rm -f *.o
```text

The `*.o` string is called a [glob](http://en.wikipedia.org/wiki/Glob_(programming)). It will match any file names which end in `.o`. This will delete all object files in the current directory.


**Wildcard expansion does not occur if you define a variable.** For this reason, if you use wildcards in variable assignments, you use the following syntax instead:

```text
objects := $(wildcard *.o)
```text

This will replace `$(wildcard *.o)` with a space-separated list of all object files in the current directory, e.g. `objects := objectfile1.o objectfile2.o`.

What is also neat is you can combine the wildcard functions with other functions for string substitution and analysis. For example, you could create a list of "future" object files by scanning the directory for files using the wildcard function, and then substituting the `.c` for `.o`. In this way you can compile and link a whole directory of `.c` files automatically. The following example does this.

```text
objects := $(patsubst %.c,%.o,$(wildcard *.c))

foo : $(objects)
cc -o foo $(objects)
```text

## Automatic Variables

Automatic variables are another great tool to use when creating automatic makefiles. Automatic variables begin with the $ character, just like normal variables.

Here is a table some of the most useful automatic variables:

<table>
    <thead>
        <tr>
            <th>Automatic Variable</th>
            <th>Comment</th>
        </tr>
    </thead>
<tbody>
<tr>
            
<td >$@</td>
<td >The file name of the target of the rule.</td>
</tr>
<tr>
<td>$%</td>
<td >The target member name, when the target is an archive member.</td>
</tr>
<tr >
<td >$<</td>
<td >The name of the first prerequisite.</td>
        </tr>
        <tr >
            
<td >$?
</td>
            
<td >The names of all the prerequisites that are newer than the target, with spaces between them.
</td>
        </tr>
        <tr >
            
<td >$^
</td>
            
<td >The names of all the prerequisites, **even if they are not newer than the target**, with spaces between them. **Does not contain any order-only prerequisites!**
</td>
        </tr>
        <tr >
            
<td >$|
</td>
            
<td >The names of all of the order-only prerequisites, with spaces between them.
</td>
        </tr>
    </tbody>
</table>

Automatic variables are used frequently in the compiler command that is executed when a rule is matched.

## Including One Makefile In Another

Note that this is different from Calling One Makefile From Another.
  
A Makefile (or a partial Makefile) can be included in another with the -include directive.

## Calling One Makefile From Another

Note that this is different from Including One Makefile In Another.

You can easily call one makefile from another. This is useful when you have a project which is made up of smaller sub-projects, and each one of the sub-projects has it's own makefile.

The recommended to run another makefile is to write:

```text
# Run another makefile from this makefile
$(MAKE) -C ./path/to/makefile/ all
```text

where all can be substituted for any other parameter you wish to pass to the secondary makefile. Note that this method is preferred over manually changing directory and calling make yourself, which can be done in the following manner:

```text
subsystem:
    cd subdir && $(MAKE)
```

The && is so that make will only be called if cd is successful. If this wasn't there and cd was not successful, make would be called in the wrong directory.

## Debugging

Make prints out some debug information to the standard output when it is run. If you want more debugging functionality, try [Remake](http://bashdb.sourceforge.net/remake/), which is a patched version of GNU Make with better error reporting, and trace execution/debugging capability.

## More Reading

For a comprehensive reading, checkout the [GNU 'make' manual](http://www.gnu.org/software/make/manual/make.html#Rules).
