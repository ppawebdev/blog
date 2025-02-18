---
authors: [ "Geoffrey Hunter" ]
date: 2013-03-18
draft: false
title: Reducing Code Execution Time
type: page
---

## Multiplication And Division

Fixed multiplication and division can converted to bit shifting to optimise code. The bit shifting operations can be found by doing a Taylor's expansion of the equation. The error in the result depends on how many bit shifting operations you wish to perform. The below example uses bit shifting instead of fixed-number multiplication to reduces the number of execution cycles, and shows the difference and error between the result and the actual value.

```c    
// Want to calculate output = 2*sqrt(2)*input
// This bit-shifting performs output = 2*input + input/2 + input/4 + input/16 + input/64,
// which is the Taylor's expansion of the above equation
output = (input<<1) + (input>>1) + (input>>2) + (input>>4)+ (input>>6);

// input = 1 -> output = 2.828125
// 2*sqrt(2)*1 = 2.828427125
// difference = 0.000302125
// error = 0.011%
```

## Powers And Square Roots

`pow()`, a function provided with most IDEs, is a slow function. If raising to the power of an integer, multiply the variable by itself rather than use the `pow()` function.

```c    
// Want to calculate output = 2*sqrt(2)*input
// This bit-shifting performs output = 2*input + input/2 + input/4 + input/16 + input/64,
// which is the Taylor's expansion of the above equation
output = (input<<1) + (input>>1) + (input>>2) + (input>>4)+ (input>>6);

// input = 1 -> output = 2.828125
// 2*sqrt(2)*1 = 2.828427125
// difference = 0.000302125
// error = 0.011%
```

There is a brilliant article on square root optimisation: [http://www.azillionmonkeys.com/qed/sqroot.html](http://www.azillionmonkeys.com/qed/sqroot.html)

## Fixed Point

mbedded.ninja has an open-source [fixed-point library](https://github.com/gbmhunter/MFixedPoint) (MFixedPoint) that is hosted on GitLab.

## Trigonometry

Fast and accurate sin/cos approximations can be found [here.](http://devmaster.net/forums/topic/4648-fast-and-accurate-sinecosine/)

The [CORDIC algorithm](http://en.wikipedia.org/wiki/CORDIC) can be used, which is a simple and efficient algorithm for calculating trigonometry and hyperbolic functions.
