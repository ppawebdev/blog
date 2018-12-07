---
author: gbmhunter
date: 2015-12-01 21:21:51+00:00
draft: false
title: Microstrips
type: page
url: /pcb-design/impedance-controlled-routing/microstrips
---

# Overview

Microstrips are impedance controlled transmission lines on the top or bottom layers of a PCB, where there is free space above the track, and a copper pour on the layer below the track. This is opposed to striplines, which are embedded in a middle layer of a PCB, and have a copper pour above and below them.

{{< figure src="/images/2015/12/single-ended-basic-microstrip-diagram-annotated.png" width="760px" caption="A diagram of a single-ended microstrip, with standard names for the various dimensions added."  >}}

# RFcafe Equations

To calculate the impedance of a microstrip, we need to know the following parameters of the PCB:

<p class="centered">
    \( w \) = width of the track (in meters)<br>
    \( t \) = thickness of the track (in meters)<br>  
    \( h \) = thickness (or height) of the substrate (in meters)<br>
    \( \epsilon_r \) = the dielectric constant of the PCB substrate<br>
</p>

The following equations can then be used to calculate the impedance of the microstrip. First we calculate the intermediary values `\(W\)` and `\(H\)`.

<div>$$ W = w + \frac{t}{\pi} \left[ ln\left(\frac{2h}{t}\right) = 1 \right] $$</div>

<div>$$ H = h - 2t $$</div>

Then we can calculate the effective dielectric, `\(\epsilon_{eff}\)` and then the track impedance, `\(Z\)`. There are different equations to be used depending on the ratio of `\(W\)` to `\(H\)`:

If `\( \frac{W}{H} < 1 \)`:

<div>$$ \epsilon_{eff} = \frac{\epsilon_r + 1}{2} + \frac{\epsilon_r - 1}{2}\left[\frac{1}{\sqrt{1 + 12\frac{H}{W}}} + 0.04\left(1 - \frac{W}{H}\right)^2\right] $$</div>

<div>$$ Z = \frac{60}{\sqrt{\epsilon_{eff}}} ln\left(\frac{8H}{W} + \frac{W}{4H}\right) $$</div>

If `\( \frac{W}{H} \geq 1 \)`:

<div>$$ \epsilon_{eff} = \frac{\epsilon_r + 1}{2} + \frac{\epsilon_r - 1}{2\sqrt{1 + 12\frac{H}{W}}} $$  </div>

<div>$$ Z = \frac{120\pi}{ \sqrt{\epsilon_{eff}} \left[ \frac{W}{H} + 1.393 + \frac{2}{3}ln(\frac{W}{H} + 1.444) \right] } $$</div>

Equations are from [http://www.rfcafe.com/references/electrical/microstrip-eq.htm](http://www.rfcafe.com/references/electrical/microstrip-eq.htm).

Go to [http://ninja-calc.mbedded.ninja/calc/microstrip-impedance-calculator](http://ninja-calc.mbedded.ninja/calc/microstrip-impedance-calculator) to use an online calculator which uses these above equations (part of NinjaCalc).

{{< figure src="/images/2015/12/screenshot-microstrip-impedance-calculator-ninjacalc.png" width="945px" caption="A screenshot of the 'Microstrip Impedance' calculator in the NinjaCalc web app."  >}}

# The Equations Altium Uses

The equation Altium uses (as of AD14, and in unsimplified form):

<div>$$ w = \frac{\frac{5.98h1}{e^{\frac{Z}{\frac{60}{\sqrt{\epsilon_r\left(1 - e^{\frac{-1.55*(0.00002+h1)}{h1}}\right)}}}-h2}}}{0.8} $$</div>

<p class="centered">
    where:<br>
    \(w\) = track width<br>
    \(h1\) = track to plane height<br>
    \(h2\) = track height (thickness)<br>
    \(Z\) = desired characteristic impedance<br>
    \(\epsilon_r\) = dielectric of material between track and plane<br>
</p>

Or in computer equation form:

```    
w = ((5.98*h1)/exp(Z/(60/sqrt(Er*(1-exp(-1.55*(0.00002+h1)/h1)))))-h2)/0.8
```
    
# Modes Of Propagation

The primary and desired mode of signal propagation in a microstrip is transverse electric and magnetic (TEM). Other modes are undesirable and increase the degradation of the signal, such as what occurs with microstrip dispersion (see below).

# Microstrip Dispersion

With wide microstrips that are far away from the ground plane, strange modes of propagation appear. Significant energy can now bounce between the microstrip and ground plane. Parts of the waveform that bounce between the microstrip and ground plane take longer to travel down the microstrip, distorting the waveform. This is called **microstrip dispersion**. Microstrip dispersion compounds quadratically with trace-to-ground height.

Why not then make the ground plane really close to the microstrip then? Well, the skin-effect resistance varies inversely proportional with trace width (remember that for a given impedance, if the height between microstrip and ground is decreased, the trace width also has to decrease). So there is a trade-off point where both effects are minimised to an agreeable level.

# Design Guidelines

A rule of thumb is to keep co-planar ground at least 3x the microstrip width away from the edges of the microstrip. Close, co-planar ground reduces the impedance of the microstrip. Infact, putting the ground too close to the microstrip results in you making a co-planar waveguide (CPW) instead!