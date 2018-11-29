---
author: gbmhunter
date: 2015-01-07 21:11:26+00:00
draft: false
title: Arithmetic Operators
type: page
url: /programming/languages/c/arithmetic-operators
---

# C Arithmetic Operators Cheat Sheet


<table >
<tbody >
<tr >
Symbol
Name
Description
</tr>
<tr >

</tr>
<tr >
Bit-shifting
</tr>
<tr >

<td >>>
</td>

<td >Arithmetic (signed) right shift operator.
</td>

<td >
</td>
</tr>
<tr >

<td ><<
</td>

<td >Left shift operator, this satisfies the requirements for both logical and arithmetic shifts.
</td>

<td >
</td>
</tr>
<tr >
Tenary
</tr>
<tr >

<td >?:
</td>

<td >Conditional operator.
</td>

<td >Use to write short, compact if statements as expressions.See the Conditional Operator section.
</td>
</tr>
</tbody>
</table>


# Increment/Decrement




Increment and decrement are two of the most basic operators in the C programming language. They are examples of a unary operator (an operator that only needs one variable). They are only valid on integer types and serve to increment or decrement the number by 1.




## Atomicity




The increment and decrement operators are not usually atomic! Of course, this is totally dependent on the architecture in use, but usually each involves three discrete operations, read the variable from memory, modify (add/subtract 1) and then write the variable back to memory. This can trip people up as increment and decrement operators have very little syntax, tricking you into believing it's a very simple machine instruction!




## A Clever But Misleading Use




The decrement operator can be used in a **clever but misleading** way to make it look like the C programming language has a "countdown to" operator.



    
    int x = 10;
    while(x --> 0) // This looks like C has a "countdown to" operator!
    {
       printf("x = %u\r\n", x);
    }
    
    // The above code will print 
    // x = 10
    // x = 9
    // x = 8
    // ...




As you have probably worked out, while(x --> 0) is not a "countdown to" operator but rather a decrement operator with a space (x --), followed by a greater than symbol >.




# Bitshifting




Bitshifting is the process of shifting the bits of a binary number to the left or the right. Bits which disappear of the end of the number are lost, and bits which a shifted onto the other end of the variable can be 0's or 1's, this is dependent on the compiler and the data type you are operating on. This makes them **non-circular shifts**.




Bitshifting can be used to quickly multiply/divide integers and fixed-point numbers by power's of two.




If the compiler supports it, bitshifting can also work with negative numbers (GCC supports it).



    
    // Bitshift 2 bits to the right (multiply by 2^2 = 4)
    temp = temp << 2;
    
    // Bitshiting 3 bits to the left (divide by 2^3 = 8)
    temp = temp >> 3;
    




Bitshifting by 0 does not modify the variable (and is likely to be optimised out by the compiler). Java has a logical (unsigned) right shift operator, >>> which is used to specify the the value should always be padded with 0's, and not whatever is the most-significant bit. C (and C++) do not have this operator, and the compiler chooses which operation to do based on the data type you are operating on.




# Modulus




The modulus operator (%) returns the remainder of an integer division. and is commonly used to manipulate binary numbers (especially to get a number that loops from 0 to a set amount and back again). For example, if you had a 32-bit counter that increased by 1024 counts per second (e.g. 1 second = 1024, 2 seconds = 2048, e.t.c), you could use the modulus operator to do counter % 1024 to return a number that varied from 0-1023 each second.



    
    // Code demonstrates the useful looping property of the modulus operator
    uint32_t count = 0;
    
    while(1)
    {
       result = count % 1024;
       printf("%lu, ", result);
       count++
    }
    
    // Output would be 0, 1, 2, ..., 1022, 1023, 0, 1, ...
    




Be careful though, as modulus is NOT a fast operation. The modulus operator:



    
    C = A % B
    




is the equivalent of:



    
    C = A – B * (A / B)
    




As you can see, everytime you use the modulus operator, you are telling the processor to do these three operations (there are exceptions however, when it comes to optimising). This can be very taking, especially on embedded systems which don't have native multiplication or division support (e.g. Atmel AVR, TI MSP430). The article, [Efficient C Tip #13 – Use The Modulus (%) Operator With Caution](http://embeddedgurus.com/stack-overflow/2011/02/efficient-c-tip-13-use-the-modulus-operator-with-caution/) explains this in more detail.




## Modulus On Floats




The modulus operator is only supported for integer data type. However, there is a standard library function for performing the modulus operation on floats and doubles, called fmod().