---
author: gbmhunter
date: 2013-11-19 04:17:18+00:00
draft: false
title: C2000
type: page
url: /programming/cpu-architectures/c2000
---

The C2000 is a processor architecture by Texas Instruments. It features in a range of TI microcontroller families including the Piccolo and Delfino range.




# Specs


<table style="width: 600px;" border="0" >
<tbody >
<tr >

<td >**Specification**
</td>

<td >**Value**
</td>
</tr>
<tr >

<td >Bus Size
</td>

<td >32-bit
</td>
</tr>
<tr >

<td >Floating Point Unit (FPU)
</td>

<td >Yes
</td>
</tr>
<tr >

<td >Frequency Range
</td>

<td >40-300MHz
</td>
</tr>
<tr >

<td >RAM
</td>

<td >5-516kB
</td>
</tr>
</tbody>
</table>


The C2000 has a math-optimised core and is designed for high-performance real-time operations.




# The Size Of A Byte




_**TLDR: The size of a byte on the C2000 is 16 bits.**_




The C2000 is somewhat unusual in that the smallest addressable memory unit is 16-bits. The C standard specifies that sizeof must return the number of bytes required to store an object, and it also stipulates that size(char) must equal 1. Because char's are stored in 16 byte memory locations (to make them separately addressable), this means that the size of a byte on the C2000 architecture is 16 bits!