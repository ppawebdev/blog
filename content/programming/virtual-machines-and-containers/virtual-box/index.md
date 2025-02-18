---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Virtual Machines And Containers" ]
date: 2013-05-23
draft: false
lastmod: 2019-07-24
tags: [ "virtual machine", "Oracle", "VM", "VirtualBox", "Linux", "shared folders", "Xubuntu" ]
title: "VirtualBox"
type: page
---

## Overview

VirtualBox is virtual machine software by Oracle.

## gedit "File Busy" Error

A long-standing bug with Oracles VirtualBox and the popular Linux text editor, Gedit (or any other text editor, for that matter), is the "File Busy" error that you get when trying to save a file across a mounted, shared folder from within Linux system running Gedit (e.g. saving into a Windows-hosted folder).

{{< img src="gedit-save-to-shared-virtual-box-folder-text-file-busy-error.png" caption="The workaround, to enable the 'Save Backup Copy' option in the preferences, and hit the save button twice."  width="800px" >}}

The problem comes from shared folders which are mounted using the command:

{{< highlight bash >}}
$ sudo mount -t vboxsf shared-name folder-to-mount-to
{{< /highlight >}}

The only workaround I am aware of is to enable the "Save Backup Copy" option in the preferences, and hit the save button twice. Annoying and far from perfect, but you can get quick at doing this (`Ctrl-S`, `Enter`, `Ctrl-S` does the trick).

{{< img src="gedit-preferences-enabling-save-backup-copy-to-stop-file-busy-error.png" caption="The 'File Busy' error that you get when trying to save a file across a mounted, shared folder from within Linux system running Gedit."  width="500px" >}}

You will also have to delete all the `.goutputstream-XXXXXX` files that are created in the directory (these are the backup files).

## SVN In Shared Folders

SVN can throw <code>svn: Can't move '.svn/tmp/entries' to '.svn/entries': Operation not permitted.</code> errors when attempting to checkout a SVN repository into a shared folder when using VirtualBox.

One work around it to use <code>git-svn</code> (install with <code>sudo apt-get install git-svn</code>) to clone the SVN repository instead.

{{< highlight bash >}}
git svn clone https://svn-repository local-folder
{{< /highlight >}}

Cloning a SVN repo using <code>git-svn</code> can take some time!

## A Lightweight Linux Distro To Run Under VirtualBox

Since Ubuntu 16.04 and upwards, I have found it to run increasingly slower when running it inside VirtualBox. This occurs even when I'm running VirtualBox on a pretty powerful Windows host with hardware-based graphics acceleration). I think this is likely due to the higher performance requirements for the Ubuntu desktop UI (transparency and other visual effects have been added). 

Because of this, I searched for a lighter-weight Linux distribution for general purpose use. I settled on [Xubuntu](https://xubuntu.org/). It offered good functionality (you can install Ubuntu/Debian packages), and runs smoothly (it no longer takes seconds to load up a terminal window!).
