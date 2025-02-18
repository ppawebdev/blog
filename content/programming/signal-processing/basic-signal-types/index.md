---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Signal Processing" ]
date: 2019-04-23
description: "A tutorial on the basic types of signals/waveforms you will come across in engineering."
draft: false
lastmod: 2019-04-29
tags: [ "signals", "sinusoidal", "unit-step function", "Heaviside", "exponential", "unit-impulse function", "waveform", "complex numbers", "Euler's formula" ]
title: "Basic Signal Types"
type: "page"
---

## Overview

This page serves to be a tutorial on the basic types of signals/waveforms you will come across in engineering.

All usages of trigonometric functions such as `\(\sin()\)` and `\(\cos()\)` below assume **angles measured in radians, not degrees**.

This page assumes basic understanding of trigonometry and complex numbers.

## Real Sinusoidal Signals

A real sinusoidal signal has the general form:

<p>$$ f(t) = A \sin ( \omega t + \theta ) $$</p>

<p class="centered">
  where:<br/>
  \(A\), \(\omega\), and \(\theta\) are real numbers
</p>

An example sinusoidal where `\( f(t) = 2\sin(2t + \frac{\pi}{4}) \)` is shown below:

{{% img src="examples-of-basic-sinusoidal-signals.png" width="700px" %}}

{{% note %}}
`\(\sin()\)` in the above equation may be replaced by `\(\cos()\)`, which just shifts everything by `\(\frac{\pi}{2}\)` (`\( \cos(x) = \sin(x + \frac{\pi}{2})  \)`). It is still called a sinusoidal signal.
{{% /note %}}

`\(A\)` controls the amplitude of the signal. A negative number will invert the signal. A value of `\(A = 1\)` will give an amplitude of `\(1\)`. 

`\(\omega\)` controls the period/frequency of the signal. A value of `\(\omega = 1\)` gives a period of `\(2\pi\)`. Doubling `\(\omega\)` doubles the frequency.

`\(\theta\)` controls the offset of the signal along the x-axis. A positive value shift the signal to the left, a negative value shifts the signal to the right.

**Sinusoidal signals normally arise in systems that conserve energy**, such as an ideal mass-spring system (no damper or frictional forces!), or an ideal LC circuit (no resistive losses).

Complex sinusoidal signals are introduced after exponential signals are explained.

## Exponential Signals

The general form for an exponential signal is:

<p>$$ f(t) = Ae^{\lambda t} $$</p>

<p class="centered">
  where:<br/>
  \(A\), \(\lambda\) are complex numbers
</p>

### Real Exponential Signals

Below are some examples of real exponential signals, showing how varying `\(A\)` and `\(\lambda\)` (limited to real numbers only) effect the waveform shape.

{{% img src="examples-of-basic-real-exponential-signals.png" width="700px" %}}

When `\(\lambda > 1\)`, the signal exhibits _exponential growth_ (this typically represents an _unstable_ signal). When `\(\lambda < 1\)`, the signal exhibits _exponential decay_ (this typically represents a _stable_ signal).

### Complex Exponential Signals

If the restriction that `\(A\)` and `\(\lambda\)` must be real numbers is removed from the general form for an exponential signal, and they are now complex numbers, a different class of signals arise. We substitute `\(\lambda\)` in the general form for a exponential signal for the complex number `\(z = \sigma + i\omega \)` to give:

<p>$$ f(t) = Ae^{(\sigma + i\omega)t} $$</p>

<p class="centered">
  where:<br/>
  \(\sigma\) is the attenuation constant<br/>
  \(\omega\) is the angular frequency
</p>

Recap Euler's formula:

<p>$$ e^{it} = \cos(t) + i\sin(t) $$</p>

Also,

<p>$$ A = |A|e^{i\theta} $$</p>

This allows us to separate out the real and imaginary parts into individual terms:

<p>\begin{align}
f(t)  &= Ae^{\lambda t} \\
      &= |A|e^{i\theta}e^{(\sigma + i \omega)t} \\
      &= |A|e^{i\theta}e^{\sigma t + i \omega t} \\
      &= |A|e^{i\theta}e^{\sigma t}e^{i \omega t} \\
      &= |A|e^{\sigma t}e^{i (\omega t + \theta)} \\
      &= |A|e^{\sigma t} \cos(\omega t + \theta) + i |A|e^{\sigma t} \sin(\omega t + \theta)
\end{align}</p>

Below are graphs of the real component of both growing and decaying complex exponential signals. **You can see how the signal is enveloped by `\(\pm |A|e^{\sigma t}\)`**. This is because the signal is the product of an exponential component and a `\(\cos()\)` component, and the `\(\cos()\)` component always varies between `\(-1\)` and `\(1\)`.

{{% img src="complex-exponential-signals-real-component-growing.png" width="700px" caption="The real component of a growing complex exponential signal. In this case \(|A| = 1, \sigma = 0.2, \omega = 2\pi , \theta = 0\)." %}}

{{% img src="complex-exponential-signals-real-component-decaying.png" width="700px" caption="The real component of a decaying complex exponential signal. In this case \(|A| = 7, \sigma = -0.2, \omega = 2\pi , \theta = 0\)." %}}

## Heaviside (Unit-Step) Function

The **Heaviside function**, named after [Oliver Heaviside](https://en.wikipedia.org/wiki/Oliver_Heaviside) (also known as the **unit-step function**) can be defined as:

<p>$$
f(t) =
\begin{cases}
0, & \text{for $t < 0$} \\
1 & \text{for $t > 0$}
\end{cases}
$$</p>

The Heaviside function looks something like the signal below, however the point at `\(H(0)\)` can be drawn in different ways (more on that below):

{{% img src="the-unit-step-function-heaviside.png" width="700px" %}}

Oliver Heaviside used his equation to calculate the current in an electrical circuit when it is first switched on {{< bib id="heaviside-wikipedia" >}}.

### The Different Conventions For H(0)

The value of Heaviside function at 0 (`\(H(t)\)` at `\(t = 0\)`) depends on the implementation or use of the function. The different values are described below. However, it is worth noting that **the value of `\(H(0)\)` is of no importance for most use cases of the Heaviside function**, as it is commonly used as a windowing function in integration (or distribution).

**H(0) = 0**

<p>$$
H(t) =
\begin{cases}
0, & \text{for $t <= 0$} \\
1 & \text{for $t > 0$}
\end{cases}
$$</p>

This is how the NIST DLMF (_Digital Library of Mathematical Functions_) defines the Heaviside function (see [section 1.16.13](https://dlmf.nist.gov/1.16#E13)). This version of the Heaviside function is left-continuous at `\(t = 0\)` but not right continuous.

{{% img src="heaviside-unit-step-function-h0-eq-0.png" width="500px" %}}

**H(0) = 0.5**

If the convention `\(H(0) = 0.5\)` is used, the Heaviside function defined as:

<p>$$
H(t) =
\begin{cases}
0, & \text{for $t < 0$} \\
\frac{1}{2}, & \text{for $t = 0$} \\
1 & \text{for $t > 0$}
\end{cases}
$$</p>

This is the version of the Heaviside function which seems to be most often used. The [Numpy documentation](https://docs.scipy.org/doc/numpy/reference/generated/numpy.heaviside.html) for `numpy.heaviside()` states that `\(H(0) = 0.5\)` is often used. This format of the Heaviside is also closely related to the [signum function](https://en.wikipedia.org/wiki/Sign_function) (the function used to extract the sign of a real number), by the following equation (shifted up by 1 and then halved in magnitude):

<p>$$ H(t) = \frac{1 + sgn (t)}{2} $$</p>

Drawn on a graph it looks like:

{{% img src="heaviside-unit-step-function-h0-eq-0p5.png" width="500px" %}}

**H(0) = 1**

<p>$$
H(t) =
\begin{cases}
0, & \text{for $t < 0$} \\
1 & \text{for $t >= 0$}
\end{cases}
$$</p>

`\(H(0) = 1\)` is how ISO 80000-2:2009 defines the Heaviside function {{< bib id="ref-iso-80000" >}}. This version of the Heaviside function is right-continuous at `\(t = 0\)` but not left continuous. It also allows the Heaviside function to be defined as the integration of the unit impulse (Dirac delta) function:

<p>$$ H(t) = \int_{-\infty}^{t} \delta(x) dx $$</p>

Drawn on a graph it looks like:

{{% img src="heaviside-unit-step-function-h0-eq-1.png" width="500px" %}}

The Heaviside function is usually defined like this when used in the context of cumulative distributions for statistical purposes. 

**H(0) = [0, 1]**

`\(H(0) = [0, 1]\)` is when the Heaviside equals both `\(0\)` and `\(1\)` (a set) at `\(t = 0\)`. This approach is not as common, but is used in optimization and game theory{{< bib id="ref1" >}}.

Drawn on a graph it looks like:

{{% img src="heaviside-unit-step-function-h0-eq-set-0-1.png" width="500px" %}}

### Shifted Heaviside

TODO

## Unit Impulse (Dirac Delta) Function

The unit-impulse function (known as a the _Dirac delta function_ in the mathematical world) is defined as:

<p>$$
f(t) = 0 \text{ for } t \neq 0 \text{ and} \\
\int_{- \infty}^{\infty} f(t) dt = 1
$$</p>

The unit-impulse function is `\(0\)` everywhere except for `\(t = 0\)` where it is infinite.

## References

<ul id="bib-list">
  <li id="ref1"><a href="https://www.quora.com/What-is-the-value-of-the-unit-step-function-at-T-0">https://www.quora.com/What-is-the-value-of-the-unit-step-function-at-T-0</a></li>
  <li id="ref-iso-80000"><a href="https://www.iso.org/standard/31887.html">https://www.iso.org/standard/31887.html</a></li>
  <li id="heaviside-wikipedia"><a href="https://en.wikipedia.org/wiki/Oliver_Heaviside">https://en.wikipedia.org/wiki/Oliver_Heaviside</a></li>
</ul>