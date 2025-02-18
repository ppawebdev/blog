---
authors: [ Geoffrey Hunter ]
categories: [ Electronics, Electronic Components, Diodes ]
date: 2011-09-05
description: Info about diodes.
draft: false
lastmod: 2022-04-28
tags: [ electronics, diodes, components, schematic symbols, TVS, ESD ]
title: TVS Diodes
type: page
---

## Overview

TVS (transient voltage suppressor) diodes are used to protect traces from high voltage spikes. They are designed to be operated in the reverse direction and work by shunting currents when the reverse voltage exceeds the **avalanche breakdown potential**. They are basically **high-power Zener diodes**, and are a specialized form of an _avalanche diode_.

They are part of a family of components used for ESD (electro-static discharge) protection, which also includes Zener diodes (however, ESD is not the only thing Zeners are used for). TVS diodes can handle large amounts of peak power (hundred's or thousands of Watts), but Zeners have a tighter voltage tolerance. TVS diodes have more capacitance than Zeners, which could be detrimental in some circumstances (e.g. when protecting the gate signal on a MOSFET).

They come in either uni-directional or bi-directional flavours. Uni-directional TVS diodes block up to the rated voltage in one direction, and behave like a normal conducting diode in the other. Bi-directional block up to the rated voltage in both directions (good for protecting AC waveforms). Use uni-directional diodes if possible, they are cheaper, and they have much faster turn-on times than their bi-directional counterparts (e.g. 4ps compared to 4ns).

## Schematic Symbol

{{% img src="tvs-diode-schematic-symbol.svg" width="400" caption="My preferred schematic symbol for a uni-directional TVS diode (or any other type of avalanche diode for that matter). Notice the double bar distinguishing it from a Zener diode symbol." %}}

## Arrays

TVS diodes can be grouped into IC packages called arrays. A typical schematic symbol for a diode array is shown below.

{{% img src="schematic-symbol-esd-diode-array.png" width="300" caption="The schematic symbol of a diode array, with a common anode connection." %}}

## Important Parameters

### Breakdown Voltage

* Symbol: `\(V_{breakdown}\)`
* Units: `\(V\)`

Also called the reverse breakdown voltage. This is the reverse voltage (cathode-to-anode) at which the diode "begins" to conduct. The point at which the diode begins to conduct is usually specified as a fixed current, typically 1mA.

### Rated Power

* Symbol: `\(P\)`
* Units: `\(W\)`

The maximum power the TVS diode can dissipate, for a specified time period. Typical values range between 400W-1.5kW.

### Standoff Voltage

* Symbol: `\(V_{standoff}\)`
* Units: `\(V\)`

This is the reverse voltage that the diode can withstand without drawing "any" current. This is one of the most important parameters, as you usually match this voltage to the maximum operating voltage of the wire you are connecting it to. Note that there is a small amount of current drawn at this voltage, this is called the reverse leakage current.

### Leakage Current

The reverse-leakage of TVS diodes decreases as the stand-off voltage increases. Be warned, the leakage current of TVS diodes which have low voltage stand-offs (e.g. <10V), can have large leakage currents! A 5V stand-off TVS diode typically has a reverse-leakage current of around 500uA, but TVS diodes with a stand-off voltage of 10V or higher have a reverse-leakage of 1uA or less. Note that at low stand-off voltages, the leakage current of a bi-directional diode can be double that of a uni-directional diode for the same stand-off voltage.

{{% img src="leakage-currents-of-tvs-diodes-with-low-standoff-voltage.png" width="1182" caption="Leakage currents of TVS diodes with low stand-off voltages." %}}

For more information, see the [ESD Protection](/electronics/circuit-design/esd-protection) page.

## Reverse Polarity Protection

Unusually, TVS diodes. along with a fuse or other current-limiting device, can act as a **very good reverse-polarity protection mechanism** on inputs to a PCB. They are usually present on a voltage rail input for the primary reason of reducing ESD. However, if the V+ and GND are connected to the PCB the wrong way around, the TVS diode will forward conduct and clamp the voltage to a normally non-destructive 0.7-1.5V. A current-limiting device like a fuse also has to be present to prevent the TVS diode from overheating.

They are especially suited to this role (when considering other diodes) as the are usually built to dissipate large amounts of heat.

{{% img src="tvs-diode-for-reverse-polarity-protection.png" width="700" caption="A TVS diode (along with a fuse) can also be a good mechanism for reverse-polarity protection." %}}

In the schematic above, the **fuse will quickly blow** if the power supply is connected to the input connector the wrong way around.

## Low Capacitance

There are a family of TVS diodes called low-capacitance (or ultra-low) TVS diodes. They have much less capacitance than standard TVS diodes (typical capacitances are between 0.4-0.9pF), and are designed for protecting high-speed data lines such as those used in USB, HDMI, DisplayPort, and Ethernet communication protocols and also for RF antennas such as GPS, FM radio and NFC antenna lines.

This low capacitance is achieved by adding a forward-biased general purpose diode in series with the usual reverse-biased TVS (zener-style diode). The schematic symbol for a low-capacitance TVS diode is shown below:

{{% img src="internal-schematic-of-low-capacitance-tvs-diode-annotated.png" width="500" caption="The internal schematic of a low-capacitance TVS diode, showing the forward-biased general purpose diode added in series to greatly reduce the total capacitance of the component." %}}

The forward-biased general purpose diode has a much smaller parasitic capacitance than the zener diode. Because the parasitic capacitances are in series (grey capacitors in diagram), the total capacitance of the component is greatly reduced!

## Special-Purpose TVS Diodes

### RS-485 TVS Diodes

TVS diodes built specifically for protecting RS-485 communication protocol bus lines are bi-directional and have two different hold-off voltages to meet the RS-485 spec. They normally include the character sequence "SM712" in their part name (e.g. SM712-02HTG by Littelfuse and SM712-TP by Micro Commerical).

{{% img src="sm712-02htg-rs485-tvs-diode-pinout-and-functional-block-diagram.png" width="500" caption="The pintout and functional block diagram of the SM712-02HTG TVS diode, designed specifically for protecting RS-485 bus lines. Image from http://www.littelfuse.com/~/media/electronics/datasheets/tvs_diode_arrays/littelfuse_tvs_diode_array_sm712_datasheet.pdf.pdf." %}}

More information on these diodes can be found in the [Specialised TVS Diodes section on the RS-485 Protocol page](/electronics/communication-protocols/rs-485-protocol#specialised-tvs-diodes).

## References

[^bib-bzx55-datasheet]:  Vishay (2019, Mar 11). _BZX55 Series Datasheet_. Retrieved 2021-09-25, from https://www.vishay.com/docs/85604/bzx55.pdf.
[^bib-vishay-1n400x-datasheet]:  Vishay (2020, Apr 29). _1N400x Datasheet: General Purpose Plastic Rectifier_. Retrieved 2021-09-26, from https://www.vishay.com/docs/88503/1n4001.pdf.
[^bib-wikipedia-crystal-detector]:  Wikipedia. _Crystal detector_. Retrieved 2021-09-26, from https://en.wikipedia.org/wiki/Crystal_detector.
[^bib-wikip-pin-diode]:  Wikipedia. _PIN diode_. Retrieved 2021-11-25, from https://en.wikipedia.org/wiki/PIN_diode.
[^bib-digikey-nte-11n4007]:  DigiKey. _NTE Electronics, Inc 1N4007_. Retrieved 2021-11-25, from https://www.digikey.com/en/products/detail/nte-electronics-inc/1N4007/11645794.
[^bib-digikey-onsemi-1n4148]:  DigiKey. _onsemi 1N4148_. Retrieved 2021-11-25, from https://www.digikey.co.nz/en/products/detail/onsemi/1N4148/458603.
