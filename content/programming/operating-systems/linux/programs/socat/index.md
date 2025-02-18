---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Operating Systems", "Linux", "Programs" ]
date: 2014-01-08
draft: false
title: socat
type: page
---

## Overview

`socat` is a very powerful utility program for establishing bi-directional data streams between two data sinks/sources. It can be used for creating two virtual COM ports that relay information to each other.

## Installation

On Debian-based operating systems (such as Ubuntu), you can type:

```sh   
$ sudo apt-get install socat
```

## Connecting Two COM Ports Together

You can use socat to connect two COM ports together. This means that any information sent to one will appear as input on the other, and vis-versa.

To set up the two-way communication, you type:

```sh    
$ sudo socat -d -d pty,raw,echo=0 pty,raw,echo=0
```

A little explanation: The `-d -d` instructs socat to print fatal, error and warning message. `pty` instructs socat to connect to a pseudo-terminal (e.g. `/dev/pts/0`, `/dev/pts/1`, ...). `raw` instructs socat to do almost not processing on input/output, and just pass it untouched. `echo=0` tells socat not to echo any input characters back to the same terminal (which is normally the desired behaviour when connecting two COM ports).

Once you type this and press enter, socat will report back with the COM ports it decided to use. The program will not return (the terminal will hang) until you wish to cancel the link (press `Ctrl-C`).

{{% warning %}}
These virtual serial ports do not fully emulate a hardware serial port. Things like baud rate, hardware flow signals e.t.c are not taken into account.
{{% /warning %}}

If you get a `bash: /dev/pts/x: Permission denied error`, run the following command:

```sh    
$ sudo chmod a+rw /dev/pts/x
```

If you want to specify the device names of the two serial ports, you can use the following command:

```sh    
$ sudo socat -d -d pty,raw,echo=0,link=/dev/ttyS10 pty,raw,echo=0,link=/dev/ttyS11
```

The above command still creates two arbitrarily named pseudo terminals in `/dev/pts/`, but it then links it to the two fixed device names provided in the command.