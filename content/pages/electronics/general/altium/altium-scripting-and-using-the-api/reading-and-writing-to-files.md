---
author: gbmhunter
date: 2015-04-28 05:52:37+00:00
draft: false
title: Reading And Writing To Files
type: page
url: /electronics/general/altium/altium-scripting-and-using-the-api/reading-and-writing-to-files
---

# Overview

You have the ability to write to and read from files inside Altium scripts. This can be useful for saving user configuration data that persists between each time the script is run, or providing input/output data for a particular script that needs to interact with the operating system.

The objects of interest are TIniFile.

TIniFile is great for storing category-key-value (or just key-value) information.

# INI Files

## Creating An INI File

You can create an INI file by using:

    var myIniFile
    myIniFile = TIniFile.Create(fileName)

where fileName is an absolute path string to the file you wish to create (e.g. C:\Users\MyUser\test.ini).

Note that "Create" is a little misleading. If the file already exists, this function performs more like "open for editing". It **does not** delete any information already present in the INI file.

## Reading And Writing To INI Files

### Booleans

You can write a boolean-based data point using:
    
    iniFile.WriteBool category, key, trueFalse

where category and key are strings, and trueFalse is a boolean.

You can read a boolean-based data point from an INI file using:
    
    Dim myBool
    myBool = myIniFile.ReadBool(category, key)

## Strings

Similarly to writing a boolean, you can write a string-based data set using:
    
    iniFile.WriteString category, key, value

where category, key and value are all strings. This will create an INI file which looks like this:
    
    [category]
    key=value

 You can read a data set from an INI file using:
    
    value = iniFile.ReadString category, key

Have a look at the file [UserData.vbs](https://github.com/mbedded-ninja/AltiumScriptCentral/blob/master/src/UserData/UserData.vbs) in the [AltiumScriptCentral repo on GitHub](https://github.com/mbedded-ninja/AltiumScriptCentral) for INI file read/write examples.