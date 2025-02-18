---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Integrated Development Environments" ]
date: 2016-06-26
description: "A tutorial on using IntelliJ, including keyboard shortcuts and how to use the IdeaVim plugin."
draft: false
lastmod: 2020-03-17
tags: [ "IDEs", "IntelliJ", "IDEA", "Java", "editor", "code", "shortcuts", "IdeaVim", "vim", "Windows", "Mac", "Python", "ssh", "deployments", "server" ]
title: "IntelliJ IDEA"
type: "page"
---

## Quick Reference

<table>
  <thead>
    <tr>
      <th>Description</th>
      <th>Shortcut</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="3"><b>Compile/Run/Debug</b></td>
    </tr>
    <tr>
      <td>Make Project</td>
      <td>
        <code>Ctrl-F9</code> (Windows)
      </td>
      <td>You can change the project settings to that artefacts (such as <code>.jar</code> files) are generated at the same time as make.</td>
    </tr>
    <tr>
      <td>Run (without debugging)</td>
      <td>
        <code>Shift-F10</code> (Windows)<br />
        <code>Ctrl-R</code> (Mac)
      </td>
      <td>Runs the last active configuration. Debugging IS NOT enabled.</td>
    </tr>
    <tr>
      <td>Run (with debugging)</td>
      <td>
        <code>Ctrl-D</code> (Mac)
        <code>Shift-F9</code> (Windows)<br />
      </td>
      <td>Runs the last active configuration. Debugging IS enabled. Note that IdeaVim on Mac can override the <code>Ctrl-D</code> shortcut to jump down half a page. You can disable this behaviour so that it "runs" instead.</td>
    </tr>
    <tr>
      <td>Step Over</td>
      <td>F8 (Windows)</td>
      <td>Use to "step over" current line of code when debugging. Step-over is one of the most commonly used debug features.</td>
    </tr>
    <tr>
      <td>Step Into</td>
      <td>F7 (Windows)</td>
      <td>Use to "step into" the current line of code while debugging. This will enter the method (if any) on the current line of code.</td>
    </tr>
    <tr>
      <td>Resume Program</td>
      <td><code>Cmd-Alt-R</code> (Mac)</td>
      <td>Continue running the program if it has been paused while debugging.</td>
    </tr>
    <tr>
      <td colspan="3"><b>View</b></td>
    </tr>
    <tr>
      <td>Show Project Window</td>
      <td><code>Alt-1</code> (Windows)</td>
      <td>Shows the file structure of the project (by default this on the left-hand side of the screen).</td>
    </tr>
    <tr>
      <td>Show Code Structure Window</td>
      <td>
        <code>Cmd-7</code> (Mac)<br>
        <code>Alt-7</code> (Windows)<br>
      </td>
      <td>This gives a great overview of the class inside the current file (e.g. it lists all the variables and methods). This shortcut will also jump the cursor to the code structure window if already open.</td>
    </tr>
    <tr>
      <td>Quick Documentation</td>
      <td><code>Ctrl-Q</code> (Windows)</td>
      <td>Great for checking up on what a class or method does as you are about to use it.</td>
    </tr>
    <tr>
      <td colspan="3"><b>Code</b></td>
    </tr>
    <tr>
      <td>Reformat Code</td>
      <td><code>Ctrl-Alt-L</code> (Windows)</td>
      <td>Corrects the coding indentation of the current file. Great for automatically tidying up code after serious refactoring has taken place.</td>
    </tr>
  </tbody>
</table>

## vim Plugin

IntelliJ supports the [IdeaVim](https://plugins.jetbrains.com/plugin/164-ideavim) plugin which adds vim-like functionality to the IDE.

This plugin supports configuration using a `~/.ideavimrc` file, which is similar in format to a typical `.vimrc` file, except that it allows special extensions to directly control IntelliJ through an API.

I have noticed that IdeaVim cannot deal with large files that well (e.g. a 50,000 line `.json` file), and I have to disable the plugin to be able to work with these files.

## Slow Deployment

One problem I have noticed in IntelliJ is the slow upload of files to a server through SSH. Even though IntelliJ was configured to only upload changed files, it was still painfully slow in uploading the 10-20 file changes that occurred whenever I switched between `git` branches. Below is an example of the slow transfer speed as reported by IntelliJ after some local files changed:

```text
[17/03/20, 4:00 PM] Automatic upload completed in 11 minutes: 64 items deleted, 374 files transferred, 14 items failed (9.7 kbit/s)
```

In the end I gave up on using IntelliJ for this and instead used `rsync`, which was about 10-100x faster.