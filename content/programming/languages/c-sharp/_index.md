---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Programming Languages", "C Sharp" ]
date: 2011-12-15
draft: false
lastmod: 2011-12-15
tags: [ "programming", "programming languages", "C Sharp", "string manipulation", "ComboBox", "GUI", ".NET", "dot net" ]
title: "C# Programming"
type: "page"
---

## String Manipulation

`<string type>.IndexOf` - Searches for a particular character within a string, and returns the position of the first instance found. Can specify where in the string to start looking, as well as how many characters to look through

`Convert.To<type>` - Converts back and forth from many standard types, including integers and strings

There is a great cheat sheet by John Sheehan which explains string manipulation in the .NET language. Unfortunately, it can no longer be found on his site, but you can still download this [locally cached version](/docs/john-sheehan-msnet-formatting-strings-cheat-sheet.pdf).

### Removing Characters From A String

`<string type>.Remove` - Removes characters from a string, starting at a specified location. Note that this creates a new string with chosen characters removed, it DOES NOT touch the original string! This is a common mistake for people to make, and results in nothing happening to the string.

```c#    
// Given string 
delSomeChars = "Blah blah blah";
// This won't work
delSomeChars.Remove(5);
// while this will
delSomeChars = delSomeChars.Remove(5);
```

### Converting To Hex

Use the `Convert.ToString()` class to convert to a hexadecimal string. The case of the format specifier (i.e. `x` or `X`), determines whether the alphabetical characters in the hex output (A-F) will be in lower-case or in upper-case.

```c#    
// Will convert the value into a hexadecimal number with 4 digits,
// (using 0 as the placeholder)
outputString = value.ToString("X4");
```

## Populating A ComboBox From An Enumeration

Populating a combo box from an enumeration can save heaps of typing and manual work to enter each item individually. It is done easily with the one line of code below:

```c#    
comboBox.DataSource = Enum.GetValues(typeof(<enumeration>));
```

You can also use the actual value of an `Enum` rather than it's name by casting it to an `int`.

## Iterating Through An Enumeration

Use the following code:

```c#    
foreach (int i in Enum.GetValues(typeof(myEnum))) {
    // Uses the enum value, i, here for your own bidding
}
```

## Running .NET On Non-Windows Platforms

There is a popular "cross platform, open source, .NET development framework" called [Mono](http://www.mono-project.com/). It is an open source implementation of the .NET framework which can run on a number of devices including Linus, Mac OS, Windows (of course), and even the [RaspberryPi](http://www.amazedsaint.com/2013/04/hack-raspberry-pi-how-to-build.html)!

## Signal Processing

The [Math.Net project](http://www.mathdotnet.com/) contains the ["Neodym" library](http://neodym.mathdotnet.com/) for signal processing in C#. See the [Signal Processing page](/programming/signal-processing/) for more information.

## Rounding

The Math library (`Math.<some function>`) supports basic rounding. However, here is a trick to round to any specified value. You basically divide the number by the precision (the number to want to round to, e.g. 0.1, 0.25, 5 e.t.c), then use standard rounding on the result, and lastly multiply the rounded number by the precision to get the answer.

```c#    
/// <summary>
/// Rounds to a given precision, using the standard Math.Round() rules. E.g. RoundToPrecision(10.34, 0.1) will return 10.3.
/// RoundToPrecision(1286, 10) will return 1290. Requires Math package.
/// </summary>
/// <param name="dataIList">Value to round.</param>
/// <param name="precision">The precision to round too. Common values are 0.1 or 0.01.</param>
/// <returns>Rounded dataIList</returns>
static public double RoundToPrecision(double value, double precision) {
    return Math.Round(value / precision, 0) * precision;
}
```

You can also preform variable precision rounding with an offset.

```c#    
/// <summary>
/// Rounds to a precision, with a given offset. Requires Math package. 
/// </summary>
/// <param name="dataIList">Value to round.</param>
/// <param name="precision">Precision to round to</param>
/// <param name="offset"></param>
/// <returns></returns>
static public double RoundToPrecision(double value, double precision, double offset) {
    return Math.Round((value-offset) / precision, 0) * precision + offset;
}
```

## Profiling And Performance Tuning

To programs to do this are SlimTune and EQATEC.

## Command-Line Parsers

Command-line parsers are a good way for user-program interaction and well as computer-computer communication. There are quite a few free and opensource C# Command-Line Parsers out there. Their core functionality is similar to the C-based linux [getopt()](http://www.gnu.org/software/libc/manual/html_node/Getopt.html) command, but incorporate the powerful functionality of the .NET language. Most use inline lambda notation to create the equivalent of call-back functions when registering the parameters.

### Command Line Parser Library

Author: [GSSCoder](https://github.com/gsscoder)
Author's Link: [https://github.com/gsscoder/commandline](https://github.com/gsscoder/commandline)
CodePlex: [http://commandline.codeplex.com/](http://commandline.codeplex.com/)
[N](https://github.com/gsscoder/commandline)uGet: "install-package CommandLineParser" (latest stable), "install-package CommandLineParser -pre" (latest release)

This library has had a continuously updated API since 2005. Parses commands in the "--age 50" style. Requires the parameters to registered with a custom class at build time.

Does not support an initial keyword that determines the nature of the following parameters (similar to calling a particular program).

### cmdline

Author: Ron Jacobs
Author's Link: [http://code.msdn.microsoft.com/Command-Line-Parser-Library-a8ba828a](http://code.msdn.microsoft.com/Command-Line-Parser-Library-a8ba828a)
NuGet: "install-package cmdline"

### NDesk.Options

Author: NDesk
Author's Link:
NuGet: 

This one can support multiple commands, with the additional library [ManyConsole](https://github.com/fschwiet/ManyConsole). NDesk.Options replaced the now obsolete Mono.Options library, and it is include in the Mono 2.0 package.

### ManyConsole

Author: [https://github.com/fschwiet](https://github.com/fschwiet)
Author's Link: [https://github.com/fschwiet/ManyConsole](https://github.com/fschwiet/ManyConsole)
NuGet: install-package ManyConsole

This library supports multiple commands, which is useful if you want to use the command-line style for communication between two computers/microcontrollers. It uses the NDesk.Options library. In my opinion, ManyConsole is hard to use, and requires all the commands/parameters to be created at compile time as classes.

## Microsoft Office Program Manipulation With C#

You can manipulate Microsoft Office applications quite easily within the .NET framework (which includes C#). See the following page I wrote for more information.

=> [Windows Office Application Interface](/programming/languages/c-sharp/windows-office-application-interface/)

## Installing Third-Party Libraries

I recommend a package manager like NuGet is used to install third-party libraries/packages whenever possible. NuGet allows you to select a pre-compiled third-part library from a large online database and then install it into a Visual Studio project at the click of a button. It also removes a library just as quickly. The image below shows the NuGet package management screen

{{< figure src="/images/programming-misc/screenshot-of-nuget-plugin-for-visual-studio.jpg" caption="A screenshot of the NuGet plugin for Visual Studio."  width="700px" >}}

## Other Resources

If you have the money, you can buy the MS Word component [Spire.Doc from E-IceBlue](http://www.e-iceblue.com/Introduce/word-for-net-introduce.html). It provides an API to easily create and manipulate Word documents in an easier manner than with Microsoft's standard library.
