---
author: gbmhunter
categories: [ "Electronics", "Test And Measurement" ]
date: 2013-10-16
draft: false
tags: [ "noise", "dB", "AC coupling", "thermal noise", "Johnson noise", "Nyquist noise" ]
title: Noise
type: page
---

## Thermal Noise

Thermal noise is generated by the random movement of charge carriers (e.g. electrons in a typical circuit) due to them having thermal energy. It is also called _Johnson_, _Nyquist_ or _Johnson-Nyquist_ noise. Thermal noise is unavoidable at any temperature except absolute zero (which is impossible to achieve).

## Measuring Noise

Use the oscilloscope trigger for viewing the noise caused by specific aggressor events. Use the oscilloscope's infinite persistence measurement to measure total noise. It is good practice to measure of a time span of many minutes with the device operating in as many of it's different states as possible.

With the oscilloscope in averaging mode and it set up to trigger of a specific event, you can view the amount of noise due to that event. Any noise asynchronous to the event will be removed through repeated averaging.

## RMS, dB, dBm, SD, Huh?

Noise measurements come in many different units. It can become very confusing when trying to compare different units or convert between them.

AC coupled waveforms become a little simpler...

> For a waveform that has no DC component, the RMS value is the same as the standard deviation.

Typically, when doing noise measurements with an oscilloscope, AC coupling is turned on, which removes the DC component. This means that the standard deviation and the RMS measurements are equal.

Uncorrelated noise sources add in a root-sum-of-squares manner.

<div>$$ e_{total} = \sqrt{e_{1}^2 + e_{2}^2} $$</div>

This comes from the equation:

<div>$$ x_{rms}^2 = \bar{x}^2 + \sigma_{x}^2 $$</div>

<p class="centered">
    where:<br>
    \( x_{rms} \) is the RMS value of waveform x<br>
    \( \bar{x} \) is the average (mean) of waveform x<br>
    \( \sigma_{x} \) is the standard deviation of waveform x<br>
</p>

As you can see, if the average of the waveform is 0 (as in the case when the waveform is AC coupled), the RMS value is the same as the standard deviation.

## Purpose-built Noise Generators

Noise generators can be built for testing circuits.