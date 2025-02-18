---
authors: [ "Geoffrey Hunter" ]
categories: [ "Electronics", "Circuit Design" ]
date: 2013-08-21
draft: false
lastmod: 2013-08-21
tags: [ "electronics", "circuit design", "thermal management" ]
title: "Thermal Management"
type: "page"
---

## Thermal Resistance

Thermal resistance is way of modelling the thermal behaviour of an object in a way analogous to calculating the current through a resistor by measuring it's voltage.

The equation is given by:

<div>$$P_D = \frac{\Delta T}{\sum R_\theta}$$</div>

<p class="centered">
	where:<br>
	\( P_D \) = Power dissipated by device (\( W \))<br>
	\( \Delta T \) = Change in temperature between both end-points<br>
	\( \sum R_{\theta} \) = The sum of thermal resistances over which \( \Delta T \) exists<br>
</p>

Which is usually expanded (and used) as:

<div>$$P_D = \frac{T_J - T_A}{R_{JC} + R_{CA}}$$</div>

If there is a heatsink involved, a new term is added:

<div>$$P_D = \frac{T_J - T_A}{R_{JC} + R_{CH} + R_{HA}}$$</div>

{{< img src="thermal-resistance-diagram-with-semiconductor.png" caption="A diagram showing how thermal resistance works. Image from http://www.aavid.com/sites/default/files/products/boardlevel/aavid-standard-heatsinks.pdf."  width="800px" >}}

An analogy to electrical resistance...

{{< img src="analogy-of-thermal-resistance-to-electrical-resistance.png" caption="The analogy of thermal resistance to electrical resistance. Image from http://www.vishay.com/docs/28705/mc_pro.pdf."  width="800px" >}}

## Inaccuracies In The Thermal Resistance Model

* Thermal resistances assume a linear relationship between temperature and heat flow. This is only a first-order approximation.

## List Of Component Package Thermal Resistances

See the [Component Packages page](/pcb-design/component-packages/). This has many of the common component packages and their thermal resistances.

Below is a condensed list of experimentally found internal thermal resistances (junction-to-case).

{{< img src="experimentally-determined-internal-thermal-resistances-for-smd-resistors.png" caption="Experimentally determined values for the internal thermal resistance (junction-to-case) for various sized SMD resistors. Image from http://www.vishay.com/docs/28705/mc_pro.pdf."  width="500px" >}}
