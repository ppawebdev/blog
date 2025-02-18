---
authors: [ "Geoffrey Hunter" ]
categories: [ "Electronics", "Electronic Components" ]
date: 2014-12-02
date: 2013-10-13
draft: false
title: Cellular Modems
type: page
---

## Overview

Most embedded modems are designed to communicate to a microcontroller over a [UART interface](/electronics/communication-protocols/uart-communication-protocol/). Some cellular modems also have embedded GPS decoders.

## Terminology

Cellular modem design is FULL of acronyms/initialisms, here is a list to help you make sense of them:

<table>
<tbody >
<tr >

<td >1G
</td>

<td >1G refers to the first generation of mobile telephone networks, one of which was NMT.
</td>
</tr>
<tr >

<td >2G
</td>

<td >2G (second-generation) is a cellular network structure. It was the first structure to be digital, and the first to allow other data aside from voice, such as SMS messages.
</td>
</tr>
<tr >

<td >2.5G
</td>

<td >See [GPRS](GPRS).
</td>
</tr>
<tr >

<td >2.75G
</td>

<td >See Edge.
</td>
</tr>
<tr >

<td >3G
</td>

<td >3G (third-generation) is a cellular network structure.
</td>
</tr>
<tr >

<td >3G+
</td>

<td >See HSDPA.
</td>
</tr>
<tr >

<td >3.5G
</td>

<td >See HSDPA.
</td>
</tr>
<tr >

<td >3GPP
</td>

<td >An initialism for the 3rd generation partnership project. The initial scope of the project was to make a globally applicable 3G mobile phone system based on evolved GSM specifications.
</td>
</tr>
<tr >

<td >3GPP2
</td>

<td >An initialism for the 3rd Generation Partnership Project 2. The projects goal was to make a globally applicable 3G cellular system within the scope the ITU's IMT-2000 project.
</td>
</tr>
<tr >

<td >4G
</td>

<td >
</td>
</tr>
<tr >

<td >A-GPS
</td>

<td >An acronym for Assited GPS.
</td>
</tr>
<tr >

<td >Antenna Diversity
</td>

<td >When a cellular modem has more than one antenna. This is to increase the chances of getting a good single when the modem is in any one position.
</td>
</tr>
<tr >

<td >CDMA
</td>

<td >
</td>
</tr>
<tr >

<td >CDMA2000
</td>

<td >
</td>
</tr>
<tr >

<td >DCS
</td>

<td >DCS is an initialism for "**digital cellular service**", which is the GSM-1800 band in the U.K.
</td>
</tr>
<tr id="EDGE" >

<td >EDGE
</td>

<td >An initialism for "enhanced data rates for GSM evolution". It is a cellular technology is a backward-compatible extension of GSM that speeds up data transmission rates.
</td>
</tr>
<tr >

<td >EGPRS
</td>

<td >See EDGE.
</td>
</tr>
<tr >

<td >FCC
</td>

<td >
</td>
</tr>
<tr id="GPRS" >

<td >GPRS
</td>

<td >
</td>
</tr>
<tr >

<td >GSM
</td>

<td >GSM is an initialism for "**Global System for Mobile Communications**". It is a standard defined by ETSI describing the 2G, 3G and 4G protocols.
</td>
</tr>
<tr id="HSDPA" >

<td >HSDPA
</td>

<td >An initialism for "high-speed downlink packet access". It is a 3G comm protocol allowing transmission speeds of up to 42.2Mbit/s. It is also called 3.5G, 3G+ or Turbo 3G. Also see HSUPA.
</td>
</tr>
<tr id="HSUPA" >

<td >HSUPA
</td>

<td >An initialism for "high-speed uplink packet access". It is a 3G comm protocol allowing transmission speeds of up to 5.76Mbit/s. Also see HSDPA.
</td>
</tr>
<tr id="IMT-2000" >

<td >IMT-2000
</td>

<td >
</td>
</tr>
<tr >

<td >IMT-SC
</td>

<td >See EDGE.
</td>
</tr>
<tr >

<td >ITU
</td>

<td >ITU is an initialism for the "**International Telecommunication Union**". They produce specifications for cellular systems such as IMT-2000 (PCS).
</td>
</tr>
<tr >

<td >LTE
</td>

<td >LTE is an initialism for "**Long Term Evolution**". It is a 4G standard for high-speed data.
</td>
</tr>
<tr >

<td >MCA
</td>

<td >MCA is an initialism for "**Mobile Communication Services On Aircraft**". It is a term used for any mobile systems operating on aircraft. It uses GSM-1800 technology.
</td>
</tr>
<tr >

<td >Microstrip
</td>

<td >
</td>
</tr>
<tr id="MO" >

<td >MO
</td>

<td >MO is an initialism for "**Mobile Originated**". It is a term used for when a SMS has been sent from a mobile device. Also see MT.
</td>
</tr>
<tr id="MT" >

<td >MT
</td>

<td >MT is an initialism for "**Mobile Terminated**". It is a term used for when a SMS has been sent to a mobile device. Also see MO.
</td>
</tr>
<tr id="NMT" >

<td >NMT
</td>

<td >NMT is an initialism for "**Nordic Mobile Telephony**" (when translated to English). It is used to refer to the first analog cellular telephone systems, also called 1G systems (this was backwards named after 2G systems came out). Two bands existed, the NMT-450 and NMT-900.
</td>
</tr>
<tr >

<td >PCS
</td>

<td >PCS is an initialism for "**Personal Communications Service**". PCS is part of the IMT-2000 standard (as defined by the ITU).
</td>
</tr>
<tr >

<td >Penta Band
</td>

<td >
</td>
</tr>
<tr >

<td >Quad Band
</td>

<td >
</td>
</tr>
<tr >

<td >SMS
</td>

<td >SMS is an initialism for "**short message servie**".
</td>
</tr>
<tr >

<td >Turbo 3G
</td>

<td >See HSDPA.
</td>
</tr>
<tr >

<td >UMB
</td>

<td >An initialism for ultra-mobile broadband.
</td>
</tr>
<tr >

<td >WCDMA
</td>

<td >
</td>
</tr>
</tbody>
</table>


## Power Supply

Most embedded cellular modems run of a supply voltage of +3.8V. Linear regulators are preferred over switching regulators as they typically have lower dropout and voltage ripple. It a switching regulator is to be used, it is preferable to use one that operates at 500kHz or above, so that it can respond to the current pulses quickly and prevent the voltage dropping to far.

A single cell Li-ion battery can also be used to power a +3.8V modem directly (with no regulator), as their voltage range falls within that acceptable for the modem. No other battery technology can be used (e.g. 4V Pb, Ni-MH or Ni-Cad) as their operating voltages either exceed or drop below that allowed by the modem.

## Rough Figures

<table>
    <thead>
        <tr>
            <th>Parameter</th>
            <th>Value</th>
        </tr>
    </thead>
<tbody >
<tr >

<td >Avergae idle current
</td>

<td >1.5mA
</td>
</tr>
<tr >

<td >Avergae transmission current at max power
</td>

<td >600mA
</td>
</tr>
<tr >

<td >Avergae transmission current at average power
</td>

<td >150mA
</td>
</tr>
<tr >

<td >Peak transmission current
</td>

<td >2A (for say, 5ms)
</td>
</tr>
<tr >

<td >Average power dissipation when using voice
</td>

<td >1W
</td>
</tr>
<tr >

<td >Average power dissipation when using data
</td>

<td >2W
</td>
</tr>
</tbody>
</table>


## SIM Cards

Listed below are the common pins that you need to connect from the SIM card (technically to the SIM card holder).

<table>
    <thead>
        <tr>
            <th>Pin</th>
            <th>Pin Type (w.r.t the modem)</th>
            <th>Description</th>
        </tr>
    </thead>
<tbody>
<tr >
<td >SIMCLK
</td>

<td >Outut
</td>

<td >The modem provides a clock signal to the SIM card through this pin.
</td>
</tr>
<tr >

<td >SIMRST
</td>

<td >Output
</td>

<td >The modem uses this pin to reset the SIM card.
</td>
</tr>
<tr >

<td >SIMIO
</td>

<td >Input/output
</td>

<td >This pin is used to send and receive data between the modem and SIM card.
</td>
</tr>
<tr >

<td >SIMIN
</td>

<td >Input
</td>

<td >This pin is used to tell the modem when a SIM card is present. It is normally used in an active low configuration.
</td>
</tr>
<tr >

<td >SIMVCC
</td>

<td >Power
</td>

<td >The pin is used to provide power to the SIM card (sometimes from the modem itself).
</td>
</tr>
</tbody>
</table>

## PCB Layout And Antenna Routing

This is the most important part of the product design!

The characteristic impedance is typically around 50Ω. The maximum allowed signal loss is normally around 0.3dB.

## Supported Bands

## GSM

GSM900/GSM1800

The GSM band is designed so that data is sent not continuously but in bursts at a rate of around 216Hz. This results in large pulse currents that can be as high as 1.5-2.0A.

## Bands By Country

Countries sorted by alphabetical order, networks sorted by technology and frequency.

<table>
<tbody >
<tr >
Country
Supported Bands
</tr>
<tr >

<td >Brazil
</td>

<td >GSM-1900, GSM-2100
</td>
</tr>
<tr >

<td >Canada
</td>

<td >
<ul>
<li>GSM-850 (rural, urban backup)</li>
<li>GSM-1900 (primary urban band, PCS)</li>
</ul>
</td>
</tr>
<tr >
<td >Japan
</td>
<td >(no GSM bands)
</td>
</tr>
<tr >
<td >Mexico
</td>
<td >GSM-1900 (PCS)
</td>
</tr>
<tr >
<td >New Zealand
</td>
<td >
<ul>
    <li>GSM-900 (Vodafone, 2degrees)</li>
    <li>GSM-1800 (Vodafone, 2degrees, only in congested areas)</li>
    <li>UMTS-850 (Telecom)</li>
    <li>UMTS-900 (Vodafone)</li>
    <li>UMTS-2100 (Vodafone, Telecom)</li>
    <li>LTE-1800 (Vodafone, only in Auckland/Christchurch)</li>
</ul>

</td>
</tr>
<tr >

<td >United States
</td>

<td>
<ul>
<li>GSM-850 (AT&amp;T Mobility, Verizon Wireless)</li>
<li>GSM-1900 (Sprint Corporation, T-Mobile US (Metro PCS))</li>
</ul>
</td>
</tr>
<tr >
<td >South Korea
</td>
<td >(no GSM bands)
</td>
</tr>
</tbody>
</table>

## Software

[Mihini](http://www.eclipse.org/mihini/) is a "M2M embeddable runtime on top of Linux". Since it requires Linux, it cannot be used in smaller embeddable projects. Code is written in the Lua language.

## Examples

The [Telit HE910 family](http://www.telit.com/en/products/umts-hsdpa.php?p_ac=show&p=108) is a series of embedded modems all within the same LGA package. Some of the models have embedded GPS decoders in them. You can get them for about US$30 in quantities of 1000.

The Simcom SIM900 is a very cheap and common place cellular modem, seen in plenty of hobbyist projects, and featuring on many Arduino/RaspberryPi shields. You can buy them for about US$18 in quantities of 1, and US$10 in quantities of 1000. The SIM900 is the most basic, but there are others in the SIM family, including the SIM908.

## Design Notes

* [Telit HE910](/electronics/components/cellular-modems/he910-design-notes)
