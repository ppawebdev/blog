---
authors: [ "Geoffrey Hunter" ]
categories: [ "Electronics", "Components" ]
date: 2011-09-03
description: "Schematic symbols, important parameters, leakage currents, failure modes, thermal stability, dead-time, FGMOS and more info about MOSFETs."
draft: false
lastmod: 2022-01-07
tags: [ "MOSFETs", "transistors", "field-effect transistors", "metal oxide semiconductors", "schematics", "electronics", "switches", "inverters", "H-bridges", "half-bridges", "switch-mode", "substrate bias effect", "floating-gate MOSFETs", "FGMOS", "EEPROM", "flash memory", "drain", "source", "gate", "split-gate", "SOA diagram" ,"safe operating area", "thermal limits", "Spirito effect", "common-source amplifier", "HEMT" ]
title: "MOSFETs"
type: "page"
---

## Overview

A _MOSFET_ (big breath now...it stands for..._Metal-Oxide-Semiconductor Field-Effect-Transformer_) is a **three-pin active semi-conductor device**, used frequently in electronics design. In the most basic sense, they can be thought of as a **voltage controlled switch** that can turn things on and off (or partially on!).

MOSFETs should not be confused with similar but different semiconductor devices such as _MODFETs_ (modulation-doped FETs) or _MESFETs_ (metal-semiconductor FETs). Depletion-mode MOSFETs are closely related to their sibling JFETs.

## Uses

* Basic electric switches (turn a load on/off)
* Totem-pole drivers
* [H-bridges](/electronics/circuit-design/h-bridges)
* 3-Phase Inverters
* Current regulating shunts (with feedback)
* [Switch-mode PSUs](/electronics/components/power-regulators)

## Types And Schematic Symbols

### Enhancement-Mode

Unfortunately for the keen circuit designer learning about MOSFETs, there is a dizzying variety of MOSFET symbols in use, owing to the fact that there are a larger number of different MOSFET types, and that no one can agree on a single standard. This section will walk you through all the various types. Firstly, [^mosfet-schematic-symbols-enhancement-mode-n-ch-p-ch] shows the commonly used schematic symbols for enhancement-mode MOSFETs, with both the N-channel and P-channel variant.

[[mosfet-schematic-symbols-enhancement-mode-n-ch-p-ch]]
{{% img src="mosfet-schematic-symbols-enhancement-mode-n-ch-p-ch.svg" width="700" caption="Schematic symbols for enhancement-mode N-channel and P-channel MOSFETs. D=drain, S=source, G=gate. This is one of the most popular variants of symbol for these device types, and contains the most information (e.g. shows the body diode, so you can't forget it exists when designing your circuit!)." %}}

WARNING: You will normally encounter P-channel MOSFET symbols with the source at the top (unlike in [^mosfet-schematic-symbols-enhancement-mode-n-ch-p-ch] where it is drawn at the bottom, just for comparison reasons with the N-channel) -- it most circuits this is the more positive node (e.g. connected to `\(V_{DD}\)`).

The arrow in the symbol has it's origins from a simple diode, in which the arrow points from the P-type substrate to the N-type substrate (which is also the direction of conventional current flow through a diode). Sometimes an **outer circle is added to the above symbols**, since a MOSFET is a transistor and by convention transistors are drawn with circles (e.g. think about a BJT symbol). However this has been omitted from the above symbols as it does contribute somewhat to the "noisyness", I find the circle-less symbol much cleaner. Totally a personal preference though.

### Depletion-Mode

Although not as popular as enhancement-mode MOSFETs, depletion-mode MOSFETs are a very important MOSFET type. They are typically distinguished on schematics from enhancement-mode types by drawing a solid line rather than a dashed line for the channel, as shown in the below figure:

image::mosfet-schematic-symbols-depletion-mode-n-ch-p-ch.svg[width=700px,link="mosfet-schematic-symbols-depletion-mode-n-ch-p-ch.svg"]

The easiest way to show the difference between enhancement and depletion-mode MOSFETs is to plot a `\(V_{GS}\)` vs. `\(I_D\)` graph as shown in [^vgs-vs-id-enhancement-and-depletion-mode].

[[vgs-vs-id-enhancement-and-depletion-mode]]
{{% img src="vgs-vs-id-enhancement-and-depletion-mode.svg" width="700" caption="Vgs vs. Id for enhancement-mode and depletion-mode N-channel MOSFETs. Fictional example (not based from real data)." %}}

The curve for the depletion-mode MOSFET is shown on the left. As you can see, the device is OFF (not conducting current) when `\(V_{GS}\)` is around `\(-4V\)` and is well and truly on when `\(V_{GS}\)` gets to `\(0V\)`. In comparison, the enhancement-mode MOSFET is fully off when `\(V_{GS} = 0V\)`, and takes around `\(+3V\)` before it starts conducting. 

Depletion-mode MOSFETs are used for:

* [^#_bi_directional_current_limiter, Bi-directional current limiting circuits (which can also withstand high voltages)]
* Current sinks/sources
* Attaching onto the input of a linear regulator to allow it to run of high voltages (or protect it from ESD)[^bib-ixys-dep-mode-mosfet-applications].

### Alternate Style #1

Sometimes the body connection, body diode and enhancement/depletion mode indicators are removed altogether from the schematic symbol, and a simplified set of symbols as below are used:

{{% img src="mosfet-schematic-symbols-simplified-style-n-ch-p-ch.svg" width="800" caption="An simplified/alternate style for a MOSFET symbol. Note the different convention used for the direction of the arrows! There is also no distinction between depletion and enhancement-mode MOSFETs in the alternative style (assume it is enhancement-mode if in doubt)." %}}

### Alternate Style #2

The difference between N-channel and P-channel MOSFETs may be instead distinguished by adding a inverting-style circle on the gate pin, this symbolises that, in a way, a P-channel is the inverse of the more typical/standard N-channel.

### CMOS 4-pin MOSFETS

MOSFETs inside ICs do not normally have the substrate connected to the source, an are instead drawn as four pin devices, of which the additional fourth pin is connected to the substrate. For N-channel MOSFETs this is typically connected to the negative voltage rail (e.g. `\(0V\)`), and for P-channel MOSFETs it is connected to the positive voltage rail (e.g. `\(V_{DD}\)`). Note also that as soon as you disconnect the substrate from the source, the drain and source pins no longer have any differences, i.e. they can be interchanged and the device will still work as expected.

## Important Parameters

Note that with all voltage parameters that mention two pins of a MOSFET (e.g. `\( V_{DS(max)} \)`), the voltage is measured with respect to the second pin (e.g. source). This would be the same as connecting the red probe of a multimeter to the drain, and the black probe to the source.

Sorted by alphabetical order, including subscripts.

### Rds(on)

`\(R_{DS(on)}\)` is the _on-state drain-source resistance_. The resistance between drain and source when the MOSFET is turned on with a strong gate drive and low `\(V_{DS}\)` (hence in the linear, Ohmic region of operation). Usually around `\(1-10\Omega\)` for smaller MOSFETs, and can be as low as `\(1m\Omega\)` for larger power MOSFETs. `\(R_{DS(on)}\)` is roughly linear with the maximum drain-source voltage of the MOSFET. For this reason BJTs or IGBTs (which both have a BJT like output) are instead preferred for high-voltage high-current applications, when the voltage starts to exceed 400V.

### Vds(max)

`\(V_{DS(max)}\)` is the _maximum drain-source voltage_. It is the maximum allowed voltage between the drain and source. A higher voltage can cause the MOSFET to breakdown. This is commonly just called the _voltage rating_ of the MOSFET, as it describes the maximum voltage it can withstand between it's "switching" terminals.

### Vgs(max)

`\(V_{GS(max)}\)` is the _absolute maximum gate-source voltage_ (aka _gate-source breakdown voltage_). Voltages above this may irreversibly destroy the MOSFET. This is due to the very thin gate-oxide layer (100nm thick, or less!) that separates the gate from the MOSFET channel, which is easily destroyed by a "high" voltage. This can be called _oxide breakdown_. `\(V_{GS(max)}\)` is very commonly `\(\pm 20V\)` for a huge variety of MOSFET families.

Because of the very high impedance of the gate pin, MOSFET devices are very sensitive to static electricity. Especially so when not soldered into any circuitry. It does not take much charge on the gate to exceed the max. gate-source voltage and destroy the MOSFET. Anti-static precautions are recommended when handling individual MOSFETs (i.e. anti-static mats, discharge wrist straps).

### Vgs(th)

`\(V_{GS(th)}\)` is the _gate-source threshold voltage_ (or just _threshold voltage_). The voltage between the gate-source at which the MOSFET begins to turn on. The point at which it "begins to turn on" is defined by the manufacturer and should be mentioned in the datasheet. Typically is is a certain drain current, e.g. `\(1uA\)`.

## How To Use Them?

The amount of current through the drain-source in controlled by a voltage on the gate. To make a basic switch, you can insert an N-Channel MOSFET between the load and ground. The source is connected to ground, and the drain to the negative terminal of the load. If the gate is given 0V (aka connected to ground), the switch will be off. If significantly more than `\(V_{GS(th)}\)` is applied to the gate, the MOSFET will fully turn on (conduct current), and the load will get power.

P-channels work in a similar manner to N-channels, the difference being that a negative `\(V_{GS}\)` has to be applied to turn them off (that is, the voltage on the gate has to be less than that on the source). This results in them commonly being used for high-side switching, in where the source is connected to `\(V_{CC}\)`, the drain to the load, and the gate voltage pulled low to turn it on, or pulled-up to `\(V_{CC}\)` to turn it off.

**In any case, do not leave the MOSFET gate floating**. Since it has a very high impedance input, if the gate is not driven, then noise can change the voltage on the gate, and cause the MOSFET to conduct/have undefined behaviour.

The above examples describing switching a MOSFET from it's fully off state to it's fully on state. But if you apply a `\(V_{GS}\)` at or just above `\(V_{GS(th)}\)`, the MOSFET will only partially turn on.

image::mosfet-vds-vs-id-for-different-vgs-showing-linear-and-saturation-regions.svg[width=500px]

WARNING: The _linear_ and _saturation_ region of a MOSFET are easy to get mixed up, and can **completely switch (ha, switch...get it?) meaning depending on the literature you're reading**! At strong gate drives and low `\(V_{DS}\)`, the MOSFET is operating in the _ohmic_ or _linear_ region, where `\( V_{DS} \propto I_D \)`. With weaker gate drive and high `\(V_{DS}\)`, the MOSFET's current `\(I_D\)` is roughly constant with varying `\(V_{DS}\)`, and is in the _saturation_ region (the current is saturated). For more discussion on this confusion, see this [StackExchange Electrical Engineering thread](https://electronics.stackexchange.com/questions/76071/meaning-of-mosfet-linear-region-in-the-context-of-switching-losses "test1").

## Leakage Current

Leakage current is an important parameter to consider when you are using the MOSFET for switching on-and-off other circuitry in a low power design. MOSFET have both a gate-to-source and a drain-to-source leakage current. Typically the drain-to-source leakage current is 10x greater than the gate-to-source leakage current. The drain-to-source leakage current increases greatly with an increase in temperature. Typical values at 25°C are `\(100nA\)` for the gate-to-source leakage current and `\(1uA\)` for the drain-to-source leakage current.

If you need lower leakage currents that what you can achieve with a MOSFET, try using a J-FET. They have typical leakage currents of `\(1-10nA\)`.

## Failure Modes

There are three ways in which a MOSFET can generally fail:

* Gate punch-through: Occurs when a large voltage spike appears on the gate that exceeds the maximum gate-source voltage (typically 10-20V). It punches a hole in the weak oxide layer.
* The drain-source voltage exceeds the rated maximum
* Overheating

To prevent over-voltage failure's, TVS diodes, Zener diodes, or snubber circuits can be used to protect the pins. TVS and Zener diodes are the most common ways to do this, and are used to clamp the voltages to a safe level.

Almost always, a MOSFET will short out the drain and source when it fails. This mean the MOSFET goes into conduction, and can destroy even more circuitry! Either make sure that your MOSFET won't fail, or take precautions against large currents if it does. I experienced plenty of MOSFET failures when designing the half-bridge for the [Electric Skateboard project](/electronics/projects/electric-skateboard)).

## Thermal Stability

The drain-source resistance of a MOSFET increases with an increase in temperature (a BJT behaves in the opposite manner, it's collector-emitter resistance decreases with an increase in temperature).

This means that MOSFETs can share current with each other easily. The positive temperature-to-resistance coefficient creates a self-balancing current mechanism for MOSFETs connected in parallel. Just make sure each MOSFET has its own gate drive resistor! Directly connected MOSFET gates can cause weird oscillation problems.

## Dead-Time

Dead-time is a technique which is commonly applied to MOSFET driving when the MOSFETs are in a H-Bridge (or half-bridge) configuration. Dead-time is the time between when one MOSFET(s) is turned off and another MOSFET(s) is turned on. It is used to prevent **shoot-through**, which is when two MOSFETs on the same leg of a H-bridge are on at the same time, creating a direct short between `\(V_{CC}\)` and `\(GND\)`. Shoot-through occurs because of the turn-off delay time of a MOSFET.

## Turn On/Turn Off Times

In precise pulse-drive situations, it is desirable for the MOSFET to have similar turn-on and turn-off times. This is so the output pulse, although delayed by these parameters, has roughly the same width as the input pulse to the gate. This is important in applications such as laser range-finding.

## Different MOSFET Construction Methods And Industry Names

_Sorted alphabetically by name._

### DMOS FET (Double-Diffused MOSFETs)

The DMOS (_Double-Diffused MOSFET_) was first developed in 1969[^bib-semantic-scholar-dmos].

### FinFETs

FinFETs are multi-fin FETs which overcome issues once MOSFET approach very small sizes (such as 22nm).

{{% img src="3d-model-of-the-structure-of-a-multi-fin-finfet.png" width="600" caption="The 3D structure of a multi-fin MOSFET (FinFET)." %}}

### FRFET

A trademarked name by Fairchild used to label some of their fast-recovery MOSFETs used in inverter and [BLDC controller](/electronics/circuit-design/bldc-motor-control) design

### HEMT

The _high-electron-mobility transistor_ (HEMT) is not technically as MOSFET, but is very closely related. It is a field-effect transistor which contains a junction between two materials with different band gaps[^bib-wikipedia-hemt].

### LDMOS (Laterally-Diffused MOSFETs)

### PROFET

A name (it stands for protected-FET) used by [Siemens](http://www.siemens.com) and now [Infineon](http://www.infineon.com) to describe power MOSFETs with built in logic circuitry for "smart switches", designed for controlling current and voltage into a load. An document about PROFETs from Infineon can be found [here](http://www.infineon.com/dgdl?folderId=db3a30431400ef68011421b54e2e0564&fileId=db3a304332d040720132f7151b4a7955).

### Trench MOSFETs

Trench MOSFETs give a very low `\( R_{DS(on)} \)` per unit silicon area.

### Gallium Nitride (GaN) MOSFETs

_Gallium Nitride_ (GaN) MOSFETs switch much faster than traditional silicon MOSFETs[^bib-ti-gan-ics], resulting in lower switch losses in power electronics and higher-frequency operation. This is because they have much smaller gate-to-drain capacitance than their silicon counterpart[^infineon-gan-hemt].

One example of a GaN MOSFET is Texas Instrument's LMG3525R030-Q1. It is a GaN MOSFET with an integrated driver, protection and error reporting. The driver supports switching speeds of up to 150V/ns[^ti-lmg352xr030-q1-ds].

<div style="display: flex;">
{{% img src="lmg3525r030-q1-ti-gan-fet-3d-render.png" width="200px" caption="3D render of the LMG3525R030-Q1[^ti-lmg352xr030-q1-ds]." %}}
{{% img src="lmg3525r030-q1-ti-gan-fet-block-diagram.png" width="200px" caption="Block diagram of the LMG3525R030-Q1[^ti-lmg352xr030-q1-ds]." %}}
</div>

## MOSFET Applications

### Load Switching

MOSFETs can be used for load switches, as shown on the [Load Switches page](/electronics/circuit-design/power-management/load-switches). They can be used in a back-to-back configuration for creating AC solid-state relays (SSRs).

{{% figure src="/electronics/circuit-design/power-management/load-switches/bjt-current-source-to-turn-p-channel-on.svg" width="500" caption="Schematic example of load switching with a P-channel MOSFET (Q2). See the [Load Switches page](/electronics/circuit-design/power-management/load-switches) for more info." %}}

Some MOSFETs designed for switching loads support logic-level inputs (e.g. +3.3V or +5.0V from either a microcontroller or logic gate) and have built in TVS diodes. One such example is the DMN61D8L-7 from Diodes Incorporated. As shown in [^dmn61d8l-7-mosfet-internal-schematic], this particular MOSFET package also included a pull-down resistor and ESD limiting resistor in series with the gate.

{{% img src="dmn61d8l-7-mosfet-internal-schematic.png" width="600" caption="Internal schematics of the DMN61D8L-7 MOSFET from Diodes Incorporated[^bib-dinc-dmn61d8l-ds]." %}}

### Isolated Gate Drives

One problem with MOSFETS (well, with any switched semiconductor) is dealing with the gate drive when either:

* A) The source voltage is not constant or at a point where the gate-source voltage for turn-on is not easy to achieve
* B) The MOSFET is dealing with large voltages and so electrical isolation between the load and the drive circuitry is desired/required (normally by law)

In these cases, the gate drive has to be **isolated**.

[IRF - Application Note AN-937 - Gate Drive Characteristics And Requirements for HEXFET Power MOSFETs](http://www.irf.com/technical-info/appnotes/an-937.pdf) is a great article on isolated gate drive techniques.

### Amplifiers

#### Common-Source Enhancement-mode MOSFET Amplifier

A _common-source enhancement-mode MOSFET amplifier_ is a basic MOSFET-based amplifier. The most popular variant is based of an N-channel enhancement-mode MOSFET (although you can make common-source amplifiers with P-channels too!), in which the source is grounded. It is **called a "common-source" amplifier because the source is a shared (common) terminal between the input and output**. It is closely related to the BJT common-emitter amplifier. Like the common-emitter amplifier, it is an inverting amplifier.

{{% img src="common-source-amplifier.svg" width="500" caption="Schematic of a basic common-mode N-channel MOSFET amplifier." %}}

The huge problem with the above circuit is the non-linearity.

### Bi-directional Current Limiter

An interesting use for [^#_depletion_mode, depletion-mode MOSFETs] is a **simple bi-directional current limiter circuit**. [^depletion-mode-mosfet-current-limiter] shows the schematic, which uses two depletion-mode MOSFETs connected back-to-back with a resistor in-between.

{{% img src="depletion-mode-mosfet-current-limiter.svg" width="600" caption="Schematic of a bi-directional current limiter made from two depletion mode MOSFETs and a resistor." %}}

The circuit above utilizes the **depletion-mode MOSFETs unique feature of being on when the gate-source voltage is 0V**. The circuit works like this:

. When no current is flowing, no voltage is dropped across the resistor. Hence both MOSFETs `\(V_{GS}\)` is 0V. Because these are depletion-mode MOSFETs, this means they are turned on, and the circuit appears as a resistance of value `\(R_S\)`.
. As current begins to flow from left-to-right, a voltage drop begins to appear across `\(R_S\)`. This creates a negative `\(V_{GS}\)` for `\(Q1\)` and a positive `\(V_{GS}\)` for `\(Q2\)`. We can ignore the positive `\(V_{GS}\)` as this only serves to turn `\(Q2\)` a little more (note that even if `\(Q2\)` wasn't on, it's internal body diode would conduct anyway). However the negative `\(V_{GS}\)` on `\(Q1\)` is important!
. As the current reaches a certain value, `\(V_{GS}\)` across `\(Q1\)` will become negative enough to reach it's `\(V_{GS(th)}\)` (which is between -2.1V and -1V for the BSP149[^bib-infineon-bsp149-ds]). At this point it will begin turning `\(Q1\)` off, `\(Q1\)` will begin to drop voltage across it and hence limit the current of the circuit.
. Because of the symmetry this circuit works in exactly the same way if current is flowing in the other direction (right-to-left), but with the roles of `\(Q1\)` and `\(Q2\)` reversed.

#### Worked Example of the Bi-directional Current Limiter

The figure above shows two BSP149 MOSFETs and an `\(R_S = 1k\Omega\)`.

From the datasheet of the BSP149, `\(V_{GS(th)}\)` is between -2.1V and -1V[^bib-infineon-bsp149-ds]. Unfortunately `\(V_{GS(th)}\)` is never a well defined parameter, so we'll just pick a value in the middle of `\(V_{GS(th)} = -1.5V\)`.

This means that the circuit should limit the current to approximately:

<p>\begin{align}
I_{LIM} &= \frac{\left| V_{GS(th)} \right|}{R_S} \\
        &= \frac{\left| -1.5V\right| }{1k\Omega} \\
        &= 1.5mA
\end{align}</p>

Because you can get depletion-mode MOSFETs with a maximum `\(V_{DS}\)` rating of 200-1000V, this circuit is an excellent candidate for protecting the input of something that could expect either a high positive or negative voltage.

TIP: Because of the part-to-part uncertainty in `\(V_{GS(th)}\)`, this circuit is suitable for crude current-limiting (e.g. for circuit protection) but not for designing an accurate current sink/source. 

## Internal Diodes

Because any PN junction is inherently a diode, a regular MOSFET has two of them. One of the diodes is removed when the substrate is connected to the source.

## The Internal BJT

So know we know that MOSFETs naturally have two internal diodes, did you know they also contain a BJT. The source-substrate-drain layers form either an NPN or PNP BJT. You don't normally have to worry about this "parasitic" element.

CMOS devices have PNPN structures. This forms a parasitic thyristor, which can cause latch-up.

## The Body Effect (aka The Substrate Bias Effect)

The body effect (also known as the _Substrate Bias Effect_) of a MOSFET describes how the threshold voltage of a MOSFET, `\(V_{TH}\)` is affected by the voltage difference between the substrate and source, `\(V_{SB}\)`. Because the source-to-body voltage can effect the threshold voltage, it can be thought of as a second gate, and the substrate sometimes called the _back gate_, and this effect called the _back-gate effect_.

Note that most discrete MOSFETs that you can buy internally tie the substrate to the source, meaning `\(V_{SB} = 0V\)`. This prevents any body effect from occurring.

Do you want the huge equation that tells you how the threshold voltage changes? Here you go:

<p>\begin{align}
V_{TN} = V_{TO} + \gamma (\sqrt{|V_{SB} + 2\phi_F|} - \sqrt{|2\phi_F|})
\end{align}</p>

<p class="centered">
  where:<br/>
  `\(V_{TN}\)` = the threshold voltage with substrate bias present [Volts]</br>
  `\(V_{TO}\)` = the threshold voltage for zero substrate bias [Volts]</br>
  `\(\gamma\)` = the body effect parameter</br>
  `\(V_{SB}\)` = the source to body (substrate) voltage [Volts]</br>
</p>

## The Substrate (Body) Connection

Standard MOSFETs actually have four, not three, electrical connection points. However most discrete MOSFET components only provide 3 leads from the package. This is because the substrate (body) lead, is normally connected internally to the source (as mentioned above in the _The Body Effect_ section), so you only get three external connections (_Gate_, _Source/Substrate_, and _Drain_).

NOTE: There are other types of specialty MOSFETs which have even more pins, such as current-measurement MOSFETs.

{{% img src="mosfet-four-terminal-internal-diagram.gif" width="350" caption="Internal diagram of a MOSFET showing the four connections, including the substrate (body) pin. Image from http://www.muzique.com/news/mosfet-body-diodes/." %}}

Another interesting note is that without the connection of the substrate to the source, the MOSFET source and drain connections would be identical, and there would be no need to separately identify them

**Q. Why is the substrate normally connected to the source?**

A. Because when it isn't, a MOSFET becomes much harder to use. If the substrate is not connected to the source, you have to consider the _body effect_. It is easier/better to connect the substrate to ground internally (less connection resistance, one less lead, e.t.c) rather than to leave it up to the circuit designed to connect it externally. Manufacturers of ICs with integrated MOSFETs may choose to connect the substrate to something else. A common choice is ground.

The 3N163 is an example of a MOSFET which provides you with a fourth pin for the substrate connection.

{{% img src="3n163-mosfet-drawing-with-substrate-connection.png" width="350" caption="A drawing of the 3N163 P-channel MOSFET, which has a fourth leg for the substrate connection (C). Image from http://pdf1.alldatasheet.com/datasheet-pdf/view/123459/CALOGIC/3N163.html." %}}

You may also note that some IC designs do not connect the substrate to the source. The TPS2020 load switch by Texas Instruments is one example. You can see in the diagram below that the substrate pin is connected to ground. I'm not entirely sure why, but it might have something to do with the devices ability to block reverse current. Normally this is achieved with back-to-back MOSFETs, but this diagram almost suggests that they pull it off using only the one MOSFET.

{{% img src="tps2020-functional-diagram-with-mosfet-body-grounded-annotated.png" width="600" caption="Functional block diagram of the TPS2020 load switch. Note how the substrate of the MOSFET (top middle) is not connected to the source, but instead connected to ground. Image from http://www.ti.com/lit/ds/symlink/tps2020.pdf." %}}

Interestingly, the block diagram for the [NCP380 high-side load switch by On Semiconductor](http://www.onsemi.com/pub_link/Collateral/NCP380-D.PDF) may shed more light on this matter. Notice how in the image below, the substrate of the MOSFET is connected to two switches, which can either connect it to the input or the output.

{{% img src="ncp380-ncv-380-load-switch-internal-block-diagram-with-reverse-current-protection.png" width="700" caption="A functional diagram of the NCP380 high-side load switch. Note the switches connected to the MOSFET substrate which show how reverse-current protection is performed." %}}

## The Transconductance Of A MOSFET

The transconductance of a MOSFET is the ratio of a change in output current (drain-source current, `\(I_{DS}\)`) due to the change in input voltage (gate-source voltage, `\(V_{GS}\)`) over an arbitrarily small range of operation.

The range of operation has to be restricted because the transconductance of a MOSFET changes depending on the operating point.

## Spice Model

Information about the MOSFET Spice model can be found on the [Altium Simulation page](/electronics/general/altium/altium-simulation).

## Floating-gate MOSFETs

A _floating-gate MOSFET_ (FGMOS) is a type of MOSFET where the gate is completely isolated. Isolation in this sense refers to no connection via conductive materials such as copper or doped semiconductor. The gate is capacitively coupled to one or more "input gates". Because the gate is isolated (the gate can also be thought of as "floating"), any charge stored on it via the capacitive coupling remains there for a long time. This forms the basis of a _floating-gate memory cell_ which is used to provide the storage in non-volatile memory such as EEPROM and flash. The cell "remembers" the state it was last in, for long periods of time, even when power is removed from the circuit.

**How long will floating-gate MOSFETs retain their charge, if un-powered?** As of 2020, the current mass-produced, consumer grade flash memory devices and SD cards claim to have a memory retention life of approximately 10 years, if left un-powered the entire time (if periodically plugged in, these devices can re-charge and "reset" the 10-year clock).

## Split-Gate MOSFETs

A very critical parameter for a MOSFET is it's on state resistance. The easiest way to reduce this is to increase the doping concentration of the epitaxial layer[^bib-science-direct-split-gate-mosfet]. However this also decreases the breakdown voltage. The _Split Gate_ MOSFET structure is a design that has been developed to allow the on resistance to decrease whilst keeping a high breakdown voltage. Comparing a standard MOSFET with a split-gate MOSFET to which both have the same breakdown voltage, the on resistance of the split-gate MOSFET can be around 50% lower. 

## Current Sensing MOSFETs

The [IXTN660N04T4](https://www.littelfuse.com/~/media/electronics/datasheets/discrete_mosfets/littelfuse_discrete_mosfets_n-channel_trench_gate_ixtn660n04t4_datasheet.pdf.pdf) by IXYS is one example of a current-sensing MOSFET.

[On Semiconductors application note AND8093/D](https://www.onsemi.com/pub/Collateral/AND8093-D.PDF) has some great reading material on current sensing MOSFETs.

## Manufacturer Part Number Families

* **2N7002**: N-channel, 60V, 300mA MOSFET from a variety of manufacturers. 

## Part Recommendations

Link to DigiKey's (US) MOSFET selection (single/discrete): https://www.digikey.com/en/products/filter/transistors-fets-mosfets-single/278

### PMV45EN - N-Ch

* Manufacturer: NXP  
* Manufacturer Part Number: PMV45EN  
* Supplier: Element 14
* Supplier Part Number: 108-1483  
* Supplier Price: NZ$0.29 (1), NZ$0.25 (100)

The PMV45EN is a low cost, very low RDS(on) N-Channel MOSFET which I use as the work horse for most of my projects. It has an RDS(on) of only 35mOhm and is rated for a current of 5.4A. The maximum drain source voltage is 30V, making it suitable for most embedded, low voltage applications. Also in the `PMV` range is the `PMV90ENER`.

### DMN3731U - N-Ch

* Manufacturer: Diodes Incorporated
* Manufacturer Part Number: DMN3731U [(datasheet)](https://www.diodes.com/assets/Datasheets/DMN3731U.pdf)
* Package: SOT-23-3
* Suppliers:
  * [DigiKey, 31-DMN3731U-7CT-ND, NZ$0.19 (100)](https://www.digikey.co.nz/en/products/detail/diodes-incorporated/DMN3731U-7/10295271)

With an max. `\(R_{DS(ON)}\)` of `\(560m\Omega\)` when `\(V_{GS} = 2.5V\)`, this N-channel MOSFET can be directly connected to GPIO lines on a +3.3V MCU. 

## MOSFET Safe Operating Areas

*The section is in notes format and needs tidying up.*

A MOSFET's SOA (_Safe Operating Area_) is usually shown as a graph in the datasheet. The SOA graph shows which combinations of drain-source voltages and drain currents are safe and which will likely damage the MOSFET. The graph takes into account steady-state operating conditions (i.e. infinite DC current) and also pulse operation. Different areas are provided for current pulses of different lengths. SOA graphs are particular important to understand for hot-swap circuits.

Transient thermal impedance plot. This is a plot which shows how the effective thermal impedance of the MOSFET changes with a time-limited pulse of power (voltage x current). The thermal impedance reduces as the pulse period becomes shorter and shorter (these graphs usually show the change between 1us and 1s). 

For moderate `\(V_{DS}\)` voltages, manufacturers determine the lines on the SOA plot from the transient thermal impedance plot.

_Spirito effect_: Named after electronic engineer and professor [Paolo Spirito](https://ieeexplore.ieee.org/author/37282676100) who showed that as MOSFET manufacturers have pushed for lower and lower `\(R_{DS(on)}\)` values, they have also inadvertently increased the tendency for a MOSFET to fail by forming unstable hot spots. Modern-day high-spec MOSFETs are actually made of from an array of MOSFET cells on the silicon with their sources, drains and gates connected in parallel. As some cells become hotter, their threshold voltage decreases relative to the other cells, and then they conduct more current, which can lead to a thermal runaway effect, destroying the MOSFET. High-density trench-style MOSFETs are effected the most[^bib-electronic-design-the-spirito-effect].

The Spirito effect is observed at high Vds voltages and low Id currents. High Vds voltages because this results in a greater change in cell power as the cell current changes. Low Id because this gives the cells more time to thermally runaway -- at higher currents the individual cells do not get a chance to thermally runaway since the entire package quickly hits it's thermal limit.

For a really good read on the Spirito effect, see [NASA's publication: Power MOSFET Thermal Instability Operation Characterization Support](/electronics/components/transistors/mosfets/nasa-tm-2010-216684-power-mosfet-thermal-instability-operation.pdf)

{{% img src="mosfet-soa-diagram-with-annotations.png" width="700" caption="A MOSFET SOA (safe operating area) diagram, showing the different limits which bound the area." %}}

. Rds(on) Limit: When `\(V_{DS}\)` is very low, it means that the MOSFET is driven to saturation, and the MOSFET acts if it has a fixed drain-source resistance, `\(R_{DS(on)}\)`. This gives a linear relationship between voltage and current and is the limit line in the upper-left section of the SOA graph.
. Package Current Limit: MOSFET datasheets will specify a maximum current, irrespective of the amount of power dissipation. The current limit is driven by physical parts inside the package which are not the silicon MOSFET cell(s), but the surrounding lead wires, bonding clips, e.t.c. This gives the upper-centre horizontal line on the SOA graph.
. Power Limit: The power limit line is determined by the maximum power dissipation the MOSFET can handle before the junction temperature exceeds it's maximum value (typically between 100-200°C). This line is dependent on the case-to-ambient thermal resistance (which is specific to the PCB/environment the MOSFET is used in!) and ambient temperature, so the best the MOSFET manufacturer can do is assume a sensible value (and hopefully state the assumption in the datasheet).
. Thermal Instability: Thermal instability occurs at lower `\(V_{GS}\)` voltages[^bib-infineon-mosfet-safe-operating-diagram].
. Breakdown Voltage Limit: Above a certain drain-source voltage, the MOSFET experiences "breakdown" and stops working correctly. This puts a hard upper-limit on the `\(V_{DS}\)` voltage, shown by the far right vertical line on the SOA graph.

## External Resources

Fairchild's application note, [AN-558 - Introduction To Power MOSFETs And Their Applications](http://www.fairchildsemi.com/an/AN/AN-558.pdf) is a great resource when using MOSFETs for power applications.

Typical [gate drive waveforms, on richieburnett.co.uk](http://www.richieburnett.co.uk/temp/gdt/gdt2.html).

## References

[^bib-science-direct-split-gate-mosfet]: : Yu-Chin Lee, Jyh-Ling Lin (2020). _Structural optimization and miniaturization for Split-Gate Trench MOSFETs with 60 V breakdown voltage_. KeAi. Retrieved 2020-10-13, from https://www.sciencedirect.com/science/article/pii/S2589208820300041.
[^bib-infineon-mosfet-safe-operating-diagram]: : Schoiswohl, J. (2017, May). _Linear Mode Operation and Safe Operating Diagram of Power-MOSFETs_. Infineon. Retrieved 2020-10-13, from https://www.infineon.com/dgdl/Infineon-ApplicationNote_Linear_Mode_Operation_Safe_Operation_Diagram_MOSFETs-AN-v01_00-EN.pdf?fileId=db3a30433e30e4bf013e3646e9381200.
[^bib-electronic-design-the-spirito-effect]: : Schimel, Paul (2011, Oct 20). _The Spirito Effect Improved My Design—And I Didn’t Even Know It_. ElectronicDesign. Retrieved 2020-10-14, from https://www.electronicdesign.com/power-management/article/21795492/the-spirito-effect-improved-my-designand-i-didnt-even-know-it.
[^bib-semantic-scholar-dmos]: : Y. Tarui, Y. Hayashi, T. Sekigawa (1969). _Diffusion Selfaligned MOST; A New Approach for High Speed Device_. Retrieved 2021-02-18, from https://www.semanticscholar.org/paper/Diffusion-Selfaligned-MOST%3B-A-New-Approach-for-High-Tarui-Hayashi/c4ad0fa7b03e080cc027545f7152caa28633fa9a
[^bib-wikipedia-hemt]: : Wikipedia (2004, Jul 19). _High-electron-mobility transistor_. Retrieved 2021-02-18, from https://en.wikipedia.org/wiki/High-electron-mobility_transistor.
[^bib-dinc-dmn61d8l-ds]:  Diodes Incorporated (2018, Jun). _DMN61D8L/LVT: 60V N-Channel Enhancement Mode MOSFET (Datasheet)_. Retrieved 2021-10-26, from https://www.diodes.com/assets/Datasheets/DMN61D8L-LVT.pdf.
[^bib-infineon-bsp149-ds]:  Infineon (2012, Nov 28). _BSP149: SIPMOS Small-Signal-Transistor_. Retrieved 2022-01-07, from https://www.infineon.com/dgdl/Infineon-BSP149-DS-v02_01-en.pdf?fileId=db3a30433c1a8752013c1fcbb815397c.
[^bib-ixys-dep-mode-mosfet-applications]:  IXYS (2014, Mar 10). _AN-500: Depletion-Mode Power MOSFETs and Applications_. Retrieved 2022-01-07, from https://www.ixysic.com/home/pdfs.nsf/www/AN-500.pdf/$file/AN-500.pdf. 
[^bib-ti-gan-ics]: Texas Instruments. _Power management > Gallium nitride (GaN) ICs (product page)_. Retrieved 2022-05-17, from https://www.ti.com/power-management/gallium-nitride/overview.html.
[^infineon-gan-hemt]: Infineon (2022). _GaN HEMT – Gallium Nitride Transistor (product page)_. Retrieved 2022-05-17, from https://www.infineon.com/cms/en/product/power/gan-hemt-gallium-nitride-transistor/.
[^ti-lmg352xr030-q1-ds]: Texas Instruments (2021, Jun). _LMG352xR030-Q1 650-V 30-mΩ GaN FET with Integrated Driver, Protection, and Temperature Reporting (datasheet)_. Retrieved 2022-05-17, from https://www.ti.com/lit/ds/symlink/lmg3525r030-q1.pdf.
