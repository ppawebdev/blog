---
authors: [ "Geoffrey Hunter" ]
date: 2012-08-20
draft: false
lastmod: 2019-02-28
tags: [ "power", "regulator", "linear", "buck", "boost", "DC/DC", "converter", "topology", "SEPIC", "current sharing" ]
title: "Power Regulators"
type: page
---

## Overview

Power regulators aim to convert an input DC voltage into a DC output voltage. There are many different ways of doing this, an each design has its benefits and advantages. The important parameters of DC/DC converters are efficiency, output ripple, complexity, and maximum output current.

## Terminology

<table>
    <thead>
      <tr>
        <th>Term</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
        <tr>
          <td>Boost converter</td>
          <td>A DC/DC converter topology which converts an input voltage into a **higher** output voltage.</td>
        </tr>
        <tr>
          <td>Buck converter</td>
          <td>A DC/DC converter topology which converts an input voltage into a **lower** output voltage.</td>
        </tr>
        <tr>
          <td>Controller</td>
          <td>A power conversion device that requires a external switch (typically a MOSFET).</td>
        </tr>
        <tr>
          <td>Converter</td>
          <td>A power conversion device that has an integrated switch (typically a MOSFET).</td>
        </tr>
        <tr>
          <td>Cuk converter</td>
          <td>A DC/DC converter topology which converts an input voltage into either a **higher** or **lower** output voltage. A Cuk converters output voltage is opposite in polarity to it's input voltage (which is a disadvantage in most cases).</td>
        </tr>
        <tr>
          <td>Down Conversion</td>
          <td>Converting an input voltage into a lower output voltage.</td>
        </tr>
        <tr>
          <td>Ripple</td>
          <td>Used when talking about voltages and currents, it is the **absolute or percentage change in voltage or current** (max - min) over an operating cycle. You typically don't want more than 20% ripple current through an inductor (w.r.t. it's average current).</td>
        </tr>
        <tr>
          <td>SEPIC</td>
          <td>SEPIC (single-ended primary inductance converter) is a DC/DC converter topology similar to a buck-boost, which converts an input voltage into either a **higher** or **lower** output voltage.</td>
        </tr>
        <tr>
          <td>Synchronous rectification</td>
          <td>When the diode in a simple DC/DC converter is replaced with a switched MOSFET to improve efficiencies. Synchronous rectification allows DC/DC converter to climb above 90% efficiency in ideal situations.</td>
        </tr>
        <tr>
          <td>Topology</td>
          <td>The type of design/technology of the converter (e.g. a buck converter is one type of topology, while a boost converter is another.</td>
        </tr>
    </tbody>
</table>

## Topology Summary

<table>
    <thead>
      <tr>
        <th>Topology</th>
        <th>Advantages</th>
        <th>Disadvantages</th>
        <th>Comments</th>
        <th>Image</th>
      </tr>
    </thead>
<tbody>
<tr>
  <td>Linear Voltage Regulator (LDO)</td>
  <td>
    <ul>
      <li>Simple</li>
      <li>Cheap</li>
      <li>Very low output ripple</li>
      <li>Low EMI</li>
    </ul>
  </td>
  <td>
    <ul>
      <li>Inefficient</li>
      <li>Can only decrease the voltage</li>
    </ul>
  </td>
  <td>Uses transistors to create a dynamically changing resistance to drop the voltage to the required level (hence linear). Dissipates the energy as heat, and therefore is very inefficient, and limited in power. Linear regulators have very low radiated EMI because they do not have a switching element. For the very same reason they also have very low output ripple, and high PSRR (power supply rejection ratio).</td>
  <td >{{< img src="lm7805-voltage-regulator.jpg" caption="The LM7805 5V linear voltage regulator in a TO-220 package."  width="160px" >}}</td>
</tr>
<tr>
<td>Buck Converter</td>
<td>
  <ul>
    <li>Very high efficiency (>90%)</li>
  </ul>
</td>
<td>
  <ul>
    <li>Can only decrease the voltage</li>
    <li>Medium complexity</li>
    <li>High EMI</li>
  </ul>
</td>
<td>Uses an inductor, capacitor and switching element to reduce the input voltage. The alternative method to a buck converter for reducing the input voltage is a linear voltage regulator. Very high efficiencies in some cases due to the absence resistive power losses.</td>
<td>{{< img src="ptma401120-dcdc-converter-module-from-ti.png" caption="The PTMA401120 DC/DC converter module from Texas Instruments. This can convert anything from 36 to 72V down to 12V with a 1A output."  width="160px" >}}</td>
</tr>
<tr>
  <td>Boost Converter</td>
  <td>
    <ul>
      <li>High efficiency (>80%)</li>
    </ul>
  </td>
<td>
  <ul>
    <li>Can only increase the voltage</li>
    <li>Medium complexity</li>
    <li>High EMI</li>
  </ul>
</td>
<td>Uses an inductor, capacitor and switching element to increase the input voltage.</td>
<td></td>
</tr>
<tr>
  <td>Buck-Boost</td>
  <td>
    <ul>
      <li>Most flexible in terms of voltage, can either decrease or increase input voltage.</li>
    </ul>
  </td>
  <td>
    <ul>
      <li>Slightly lower efficiency than a dedicated boost or buck converter</li>
      <li>Input voltage range extremes are usually less than a dedicated buck or boost converter.</li>
      <li>High EMI</li>
      <li>Larger part count than a dedicated buck or boost converter.</li>
    </ul>
  </td>
  <td>This is basically a combination buck and boost converter in one, and so can either increase or decrease the input voltage.</td>
  <td></td>
</tr>
<tr>
<td>Charge Pump</td>
<td>
<ul>
<li>Very high efficiency (99%)</li>
<li>Simple, requires minimal external componentry</li>
</ul>
</td>
<td >
<ul>
<li>Low output current</li>
<li>High output resistance</li>
<li>Fixed output voltages</li>
</ul>
</td>
<td >Uses capacitors, diodes, and a oscillating switch to move charge from one capacitor to another, and in the process, increasing the voltage on the second cap. Normally the voltage is doubled, and multiple elements can be connected together to create larger voltage increases.
</td>
<td></td>
</tr>
<tr>
  <td> Joule Thief</td>
  <td>
    <ul>
      <li>Simple</li>
      <li>Moderately efficient</li>
      <li>Good at extracting all the energy from a power source.</li>
    </ul>
  </td>
  <td >
    <ul>
      <li>Low power</li>
    </ul>
  </td>
  <td> Used in low power and cheap applications, e.g. powering an LED from a 1.5V battery.</td>
  <td>{{< img src="joule-thief.jpg" caption="A tiny Joule Thief made for a single coin battery that can power an LED."  width="160px" >}}</td>
</tr>
</tbody>
</table>

## DC/DC Converters And Controllers

{{< img src="recom-acdc-converter.jpg" caption="A Recom AC/DC converter module that can take 100-240VAC as it's input and outputs 12V at up to 83mA."  width="200px" >}}

DC/DC converters and controllers are ICs which contain all of the logic and most of the passive componentry that makes up a switching power converter. When the industry talks about a DC/DC converter, they are talking about a chip which has an integrated switch (usually a [MOSFET](/electronics/components/transistors/mosfets/)). When they talk about a DC/DC controller, they are talking about a chip which requires an external switch.

Most DC/DC converters and controllers require at least an external input capacitor, switching inductor, and output capacitor. Some however, like Linear Technology uModule range, have the inductor/capacitors built in also. These tend to be rather expensive!

Two important patents in the history of DC/DC converters are patent [US3040271](http://www.google.com/patents/US3040271) and [US4097773](http://www.google.com/patents/US4097773).

DC/DC converters are also used to charge batteries from solar panels. In this case, they are operated in an unusual fashion, because you want to regulate the input voltage to what provides maximum power extraction from the solar panel, rather than regulating the output voltage. Sometimes AC/DC power supplies are called LPS, which is an acronym for "**limited power supply**". This term is related to the IEC60950-1 standard.

{{< img src="ul60950-limited-power-circuits-graph.png" caption="A graph of voltage vs. current for a LPS (limited power supply)."  width="400px" >}}

### Efficiencies

The efficiency of DC/DC converters can be as high as 96-98%!  You will see a figure like this quoted in most DC/DC converter IC datasheets. However, this efficiency only applies when the **converter is operating at one specific point** (the right input voltage, output voltage, load current, and temperature). Your own personal design will most likely be using the converter at a variety of different operating points, which may or may not include the one for maximum efficiency. When in actual use over a range of operating conditions, an average of about 80% efficiency is common from a good DC/DC converter. **Only use this rating for comparing the quality of one DC/DC converter against another.**

### Burst Mode

DC/DC converters can extend their efficient operating current range by enabling the converter to operate in what is called a "burst" mode at low currents. When a converter is in this mode, it provides a burst of pulses to power the output until the output voltage climbs over a set threshold, turns off, and doesn't turn back on again until the load voltage drops below a certain threshold. This turns out to be more efficient than continuous mode at low currents, but also **increases the total noise** radiated from the DC/DC converter. Most converters that employ this technique have a way of forcing the converter to stay in fixed frequency mode to reduce noise, which is useful for when powering devices such as GPS ICs.

## AC/DC Converters

Although strictly not a DC/DC converter, you can purchase ready-to-go PCB-mounted AC/DC converter modules that are designed to plug straight into the AC mains (90-270VAC(rms)), and output a DC voltage typically between 3.3 and 24V. Power ratings are typically 1-10W. The one shown below is made by MeanWell.

{{< img src="meanwell-pm-15-12-acdc-converter-size-comparison-photo.jpg" caption="Size comparison of a Meanwell 15W, 12V AC/DC converter."  width="500px" >}}

The types which are designed to be plugged straight into the wall are called wall-warts. They usually have two-core wire going to a DC jack connector. The wire with the white stripes on it is usually positive.

## Current Sharing

You can balance current-sharing between two similar power supplies by adding in-line resistance to each of power supply outputs, before connecting them together. Normally power resistors are required (>= 5W), and resistances between 1mΩ and 1Ω are used. Basically, you want to choose the largest resistance that at maximum current won't overheat, and won't drop to much voltage so that the load does not operate correctly. I have used this technique successfully for the [Luxcity UV Tonic project](/electronics/projects/luxcity-uv-tonic-control-system) to current-share between two computer power supplies that were driving the 64 solenoids.

A great technical article on current sharing can be found at <http://powerpartners-inc.com/wp-content/uploads/2018/08/Load_Sharing_Considerations.pdf>.

## Buck-Boost Converter

A buck-boost power converter is a power supply which can produce an output voltage which can be both higher or lower than the input voltage. A buck-boost converter is similar to a SEPIC converter. Buck-boosts are not used unless an output voltage which could be both lower and higher than the input voltage is specifically required, as usually a sole buck or boost converter is cheaper, has a lower part count, and is more efficient. Maxim claims that a boost with linear regulator instead of a buck circuit can out perform a buck/boost in certain applications.

## Joule Thieves

The team at RustyBolt has experimented with plenty of different Joule thief designs, and documented the results well on [their website](http://rustybolt.info/wordpress/).
