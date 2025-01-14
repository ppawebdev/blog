---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Build Systems And Package Managers" ]
date: 2017-01-30
draft: false
title: Gradle
type: page
---

## Overview

Gradle is an open-source build automation system. It is primarily targeted towards languages running on the JVM (Java Virtual Machine).

{{< img src="gradlephant-gradle-logo-v2.png" width="271px" caption="The Gradle logo." >}}

One of it's big advantages over Maven is it's use of a domain-specific language (DSL) rather than XML to specify the project configuration and build steps.

## The Java Plugin

The Java plugin is probably one of the most commonly used plugins. To use the plugin, add the following to your build script:

```
apply plugin: 'java'
```

The Java plugin assumes the same traditional layout of files that Maven did:

<table>
    <thead>
        <tr>
            <th>Directory</th>
            <th>Meaning</th>
        </tr>
    </thead>
<tbody >
<tr>
<td><code>src/main/java</code></td>
<td>Production Java source</td>
</tr>
<tr>
<td><code>src/main/resources</code></td>
<td>Production resources</td>
</tr>
<tr>
<td><code>src/test/java</code></td>
<td>Test Java source</td>
</tr>
<tr>
<td><code>src/test/resources</code></td>
<td>Test resources</td>
</tr>
<tr>
<td><code>src/_`sourceSet`_/java</code></td>
<td>Java source for the given source set</td>
</tr>
<tr>
<td><code>src/_`sourceSet`_/resources</code></td>
<td>Resources for the given source set</td>
</tr>
</tbody>
</table>

These default file locations can be changed if needed (however, it is recommended to use the default configuration unless you have good reason not to).
