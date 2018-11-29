---
author: gbmhunter
date: 2011-09-07 00:57:27+00:00
draft: false
title: TeX
type: page
url: /programming/languages/tex
---

[mathjax]




# Overview




TeX is a typesetting language for producing documents. It is one of the most popular alternatives to WYSIWYG text editors such as Microsoft Word. The language largely resembles a programming language, and is then compiled to produce professional looking documents.




The advantage of TeX typesetting over an editor such as Microsoft Word is the conformity and standardization that comes naturally when writing a document using 'code'. For example, figures are always labeled correctly and in the same manner, page margins are identical, and bibliographic references are identical and always match correctly with the reference. The large disadvantage with TeX typesetting is the lack of instant feedback (although there are some packages that now support live feedback), and the complexity in understanding and knowing how to write in the TeX language.




There is a difference between a TeX distribution and a TeX editor.




# TeX Distributions





	  * LaTeX (my favourite)



# TeX Editors





	  * MiKTeK
	  * TeXnicCenter






# MathJAX


<table >
<tbody >
<tr >
Operator
Description
Example
See Also
</tr>
<tr >

<td >\dfrac{x}{y}
</td>

<td >Prints a fraction, in display mode (normally larger than \frac{}).
</td>

<td >\(\frac{x}{y}\)
</td>

<td >\frac{x}{y}
</td>
</tr>
<tr >

<td >\frac{x}{y}
</td>

<td >Prints a fraction.
</td>

<td >\(\frac{x}{y}\)
</td>

<td >\dfrac{x}{y}
</td>
</tr>
<tr >

<td >\text{This is normal text.}
</td>

<td >Print normal text (not math-style text). This also means spaces are preserved.
</td>

<td >\(\text{This is normal text.} \\ This is maths text.\)
</td>

<td >
</td>
</tr>
</tbody>
</table>


# Example Code



    
    % Produces a matrix equation
    I_{\alpha\beta\gamma} = TI_{abc} = \frac{2}{3} \begin{bmatrix} 1 & -\frac{1}{2} & -\frac{1}{2} \\ 
    0 & \frac{\sqrt{3}}{2} & -\frac{\sqrt{3}}{2} \\ 
    \frac{1}{2} & \frac{1}{2} & \frac{1}{2} \end{bmatrix} \begin{bmatrix} I_a \\ 
    I_b \\ 
    I_c \end{bmatrix} \text{(unsimplified Clarke transform)} \\ \\
    




$$ I_{\alpha\beta\gamma} = TI_{abc} = \frac{2}{3} \begin{bmatrix} 1 & -\frac{1}{2} & -\frac{1}{2} \\ 0 & \frac{\sqrt{3}}{2} & -\frac{\sqrt{3}}{2} \\ \frac{1}{2} & \frac{1}{2} & \frac{1}{2} \end{bmatrix} \begin{bmatrix} I_a \\ I_b \\ I_c \end{bmatrix} \text{(unsimplified Clarke transform)}\\ \\ $$