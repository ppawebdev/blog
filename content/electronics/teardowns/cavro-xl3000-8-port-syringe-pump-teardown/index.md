---
authors: [ "Geoffrey Hunter" ]
categories: [ "Electronics", "Teardowns" ]
date: 2013-03-03
draft: false
lastmod: 2013-03-03
tags: [ "Cavro", "XL-3000", "syringe pump", "teardown", "electronics", "OEM", "Hamilton", "Tecan US", "Emerald Bio" ]
title: "Cavro XL-3000 8-port Syringe Pump Teardown"
type: "page"
---

This page details the teardown of a Cavro XL-3000 pump. I had an OEM model, so the exact part number of the unit was a little hard to determine. I contacted both Tecan US and Emerald Bio with a request for the Operator's manual. This is the reply I got from Tecan US.

<blockquote>Sorry Geoff, Our company works direct with OEM's, and unless you have directly purchased product from us, we are not able to help with your inquiry. Please contact company where you purchased from for support. Thank you</blockquote>

I found the schematic "[Metrolab Wiring Diagram](http://www.frankshospitalworkshop.com/equipment/documents/automated_analyzer/service_manuals/Metrolab%202300%20-%20Wiring%20diagram.pdf)" which had the following section in it.

{{< img src="m2300p-cpu-to-cavro-xl3000-schematic.jpg" caption="Image from http://www.frankshospitalworkshop.com/equipment/documents/automated_analyzer/service_manuals/Metrolab%202300%20-%20Wiring%20diagram.pdf."  width="900px" >}}

Although there was no reference to the PCB fingers on the XL3000, the pinout is strangely similar.

The Hamilton PSD/8 is meant to be a "drop in replacement" for the Cavro XL3000. So finding a manual for this would mean finding a manual for the XL3000. Unfortunately, these are really hard to come by also. I did find the [Hamilton PSD8 Syringe Pump Specification Sheet](/images/2013/03/hamilton-psd8-syringe-pump-spec-sheet.pdf), but it does not have any information on the connector wiring or commands.

Here is the [Cavro XP-3000 Syringe Pump Operators Manual](/images/2013/03/cavro-xp-3000-syringe-pump-operators-manual.pdf). The XP-3000 is the smaller cousin (30mm stroke length) of the XL-3000.

I finally got it! Thanks to Emerald Bio, who sent me the [Cavro XL-3000 Syringe Pump Operators Manual](/images/2013/03/cavro-xl-3000-syringe-pump-operators-manual.pdf) after I contacted them via email.

Pictured below is the wiring diagram for the PCB finger connector on the XL-3000.

{{< img src="cavro-xl3000-syringe-pump-wiring-diagram-for-connector.jpg" caption="The wiring diagram for the PCB finger connector on the Cavro XL-3000 syringe pump. Taken from the schematic in the operators manual."  width="800px" >}}

The bare minimum number of connections to get it working are 4, the +24V, GND, RS-485 A Line, and RS-485 B Line (or the RS-232 TX and RX line instead of the RS-485 connections if you have the RS-232 interface board attached). The +24V power supply has to be capable of providing 850mA. A USB-to-RS-485 converter is a good way to control the pump from a computer. The syringe pump is set by default to communicate at 9600 baud.

{{< img src="communicating-via-rs-485-to-syringe-pump.jpg" caption="Communicating to the syringe pump via a USB-to-RS-485 converter."  width="700px" >}}

When 24V is applied, the port motor should rotate to the start position. If it is already at the start position, it will do a full rotation anyway. I presume this is so the optical encoder can work out where the motor is.

<p>When connecting one motor, a jumper is need on <code>JP7</code> or <code>JP8</code>. They come shipped with a jumper on <code>JP7</code>. <code>SW1</code> controls the address of the pump. It should be set from <code>0x0</code> (which gives address <code>0x31</code>) to <code>0xE</code> (which gives address <code>0x3F</code>). Setting <code>SW1</code> to <code>0xF</code> makes the pump execute a self-test procedure.</p>

There are two communication protocols, the OEM protocol and the DT (data terminal) protocol. The OEM protocol is more noise resistant, has checksums, and return message formats. The DT protocol is basic and suitable for controlling directly from a data terminal. I used the following settings in the PuTTy terminal. I decided to try the DT protocol.

{{< img src="putty-configuration-for-comms-with-cavro-xl3000-syring-pump.png" caption="The PuTTY configuration settings for communicating to the syringe pump."  width="700px" >}}

Making sure the virtual COM port was installed correctly.

{{< img src="usb-serial-port-for-rs-485-converter-in-device-manager.png" caption="When installing a USB-to-RS485/422 converter, it installs a virtual COM port under the Device Manager in Windows."  width="500px" >}}

{{< img src="dip-switch-sw2-configuration-cavro-xl3000-syringe-pump.png" caption="The DIP switch settings for SW2 on the XL-3000 syringe pump"  width="80px" >}}

To get it running, the only setting I had to change was DIP switch 2 (`SW2`), from `ON` to `OFF`. This changed the message protocol from OEM to DT, allowing simple, no checksum needed comms from a terminal program on a PC.

{{< img src="the-dip-switch-sw2-on-the-syringe-pump.jpg" caption="The DIP switch (SW2) on the XL-3000 syringe pump." width="700px" >}}

<p>To get the pump to initialise, I sent the command <code>/1ZR</code>. <code>/</code> indicates that a command follows, <code>1</code> is the pump address, <code>Z</code> is the command (initialise with valve to the right), and <code>R</code> executes the command. See the datasheet for more information on the commands. You should get the response <code>/0@</code>, as shown in the image below.</p>

{{< img src="basic-message-and-response-to-xl3000-in-terminal.png" caption="Sending the initialise message to the syringe pump at the pumps response. This was using the PuTTy terminal program, with the pump in the 'RT' protocol mode."  width="700px" >}}
