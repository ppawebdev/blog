---
authors: [ "Geoffrey Hunter" ]
date: 2013-06-28
description: "A step-by-step tutorial on writing a basic Hello, World program in assembly."
draft: false
tags: [ "assembly", "hello, world", "Intel", "AT&T", "NASM", "gcc", "printf" ]
title: "Assembly"
type: page
---

<h2>Overview</h2>

<p>If you are writing assembly for ARM processors, make sure to check out the [GNU ARM Assembler Quick Reference](http://bel.gsi.de/scripts/gnu-arm-assy-quick-ref.pdf).</p>

{{< figure src="/images/2013/06/assembly-code-example.png" width="481px" caption="An example of assembly code from the glibc library (an optimised memcpy() function)."  >}}

<h2>Intel vs. AT&T Syntax</h2>

<b>Intel Syntax</b>

<p>Intel syntax always puts the destination address before the source address.</p>

{{< highlight asm >}}
instr dest, source
mov eax, [ecx]
{{< /highlight >}}

<b>A&T Syntax</b>

<p>AT&T syntax always puts the source address before the destination address. It also requires a `%` infront of every register access, and a `$` infront of immediate operands.</p>

{{< highlight asm >}}
instr source, dest
movl (%ecx), %eax
{{< /highlight >}}

<h2>NASM</h2>

<p>The NASM assembly language is a very popular language that works on the x86 and x86-64 architectures. It has similar syntax to Intel's x86/x86-64 assembly, but it designed to be more "user friendly".</p>

<b>Compiling NASM Assembly</b>

<p>You can download the NASM compiler for Ubuntu and other Debian-like systems with:</p>

{{< highlight bash >}}
$ sudo apt install nasm
{{< /highlight >}}

<p>To compile a NASM <code>.asm</code> file, first convert it to an object file with the nasm program:</p>

{{< highlight bash >}}
$ nasm -f elf test.asm
{{< /highlight >}}

<p>OR for a 64-bit object file:</p>

{{< highlight bash >}}
$ nasm -f elf64 test.asm
{{< /highlight >}}


<p>This will produce an object file called <code>myfile.o</code>.

{{% note %}}
Not all assembly instructions are supported for both 32-bits and 64-bits.
{{% /note %}}

<p>You then have two options for linking:</p>

<ul>
<li>Use the linker program <code>ld</code>.</li>
<li>Use <code>gcc</code>. This automatically links against the C standard library for you.</li>
</ul>

<p>Using gcc:</p>

<p>32-bit object files:</p>

{{< highlight bash >}}
$ gcc -m32 test.o -o test
{{< /highlight >}}

For 64-bit object files:

{{< highlight bash >}}
$ gcc -m64 test.o -o test
{{< /highlight >}}

<b>Hello World (using NASM)</b>

<p>This Hello, World example will be as bare-bones as possible, and will not even use the <code>printf()</code> function call (instead it will make a Linux system call directly).</p>

<p>First, we need a <code>.section text</code> to tell the compiler that this is our executable code.</p>

{{< highlight asm >}}
.section text
{{< /highlight >}}

<p>We then need to define an entry point for our program:</p>

{{< highlight asm >}}
    global _start
_start:
    ... more code here ...
{{< /highlight >}}

<p>Now, printing <code>Hello, world!</code> requires the use of a Linux system call to print the text to `stdout` (specifically, <code>sys_write</code>). We will use the Linux <i>fastcall</i> convention which <b>allows us to put the input arguments into registers, rather than on the stack</b>. The system call number is placed in <code>eax</code>, and the arguments in the successive registers <code>ebx</code>, <code>ecx</code>, e.t.c. The function number for <code>sys_write</code> is <code>4</code> (<a href="https://syscalls.kernelgrok.com/">see here</a>). We need to place the file we wish to write to in ebx, a pointer to the message (<code>char *</code>) in <code>ecx</code>, and the number of characters in <code>edx</code>.</p>

{{< highlight asm >}}
section .text
    global _start
_start:
    mov edx, <msg size>
    mov ecx, <pointer to msg>
    mov ebx, 1
    mov eax, 4
{{< /highlight >}}

Note that I have assigned the registers in reverse order (starting at edx and going to eax). This is not necessary (any order would work), however this practise stems from the sequence required making a system call by pushing to the stack instead, in where this order is important. I just kept the same practise for good readability.

So, now we need to place the message in memory somewhere, and also find out it's size, so we can fill in <code>&lt;pointer to msg&gt;</code> and <code>&lt;msg size&gt;</code>. We can create a data section just for this purpose:

{{< highlight asm >}}
section .text
    global _start
_start:
    mov edx, <msg size>
    mov ecx, <pointer to msg>
    mov ebx, 1  ; File descriptor 1 is stdout
    mov eax, 4  ; System call 4 is sys_write
section .data
    msg db 'Hello, world!' ; Creates a string of characters. Note: No null terminator.
    len equ $ - msg        ; Calculate the length of the string (note, this does not store anything in memory)
{{< /highlight >}}

db is a NASM instruction which stands for <i>define bytes</i>. It defines a sequence of bytes in memory. <code>equ</code> just tells the compiler to calculate the length of the message and save it to <code>len</code> (called a <i>symbol</i>), which can then be used in the code (it does not save the value to memory, it is similar to #define in C).

Lets use the new <code>msg</code> variable in our code:

{{< highlight asm >}}
section .text
    global _start
_start:
    mov edx, len
    mov ecx, msg
    mov ebx, 1  ; File descriptor 1 is stdout
    mov eax, 4  ; System call 4 is sys_write
section .data
    msg db 'Hello, world!' ; Creates a string of characters. Note: No null terminator.
    len equ $ - msg        ; Calculate the length of the string (note, this does not store anything in memory)
{{< /highlight >}}

Great, everything is setup for a system call! But how do we perform a system call? In Linux, a system call is made by triggering the <code>0x80</code> interrupt, so we will do just that:

{{< highlight asm >}}
section .text
    global _start
_start:
    mov edx, len
    mov ecx, msg
    mov ebx, 1  ; File descriptor 1 is stdout
    mov eax, 4  ; System call 4 is sys_write
    int 0x80
section .data
    msg db 'Hello, world!' ; Creates a string of characters. Note: No null terminator.
    len equ $ - msg        ; Calculate the length of the string (note, this does not store anything in memory)
{{< /highlight >}}

Running the above code should print <code>Hello, world!</code> to stdout. But your program might then just seg fault. This is because we have not exited cleanly. To do this, we can make another sys call, this time to <code>sys_exit</code> (<code>0x01</code>).

{{< highlight asm >}}
section .text
    global _start
_start:
    mov edx, len ; len was calculated in .data section
    mov ecx, msg ; Pointer to array of chars in .data section
    mov ebx, 1   ; File descriptor 1 is stdout
    mov eax, 4   ; System call 4 is sys_write
    int 0x80     ; sys call
    mov ebx, 0   ; Return code of o.k.
    mov eax, 1   ; sys_exit function number
    int 0x80     ; sys call
section .data
    msg db 'Hello, world!' ; Creates a string of characters. Note: No null terminator.
    len equ $ - msg        ; Calculate the length of the string (note, this does not store anything in memory)
{{< /highlight >}}

All done! Run this code online at [https://www.tutorialspoint.com/tpcg.php?p=qjMuBp](https://www.tutorialspoint.com/tpcg.php?p=qjMuBp).

<b>Hello World With printf()</b>

Because we want to know use a standard library function, we are going to take a slightly different approach.

Create a <code>test.asm</code> file with the following contents:

{{< highlight asm >}}
extern printf   ; Make sure to link with gcc so that standard library is automatically linked against

SECTION .data
msg: db "Hello, world!",0xA,0x0     ; 0xA = new line, 0x0 = end of string

SECTION .text                       ; Code section

global main
main:               ; The program label for the entry point
    push ebp        ; Save stack base pointer
    mov ebp, esp    ; Move stack pointer onto stack base pointer
    push msg        ; Last thing on stack is printf formatting string
    call printf

    mov esp, ebp    ; Unwind stack
    pop ebp         ; Replace base pointer

    mov eax,0       ; Return error code of 0 (no error)
    ret             ; Return from main()
{{< /highlight >}}

Now compile and run with the following commands:

{{< highlight bash >}}
$ nasm -f elf test.asm
$ gcc test.o -m32 -o test
$ ./test
Hello, world!
{{< /highlight >}}
