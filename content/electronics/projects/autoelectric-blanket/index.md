---
authors: [ "Geoffrey Hunter" ]
categories: [ "Projects", "Electronics" ]
date: 2015-10-04
tags: [ "electric blanket", "project", "smart phone", "IoT" ]
title: Autoelectric Blanket
type: page
---

## Overview

To design a smart phone controlled electric blanket.

## Material Costs

<table>
  <thead>
    <tr>
      <th>Item</th>
      <th>Cost (NZ$)</th>
    </tr>
  </thead>
<tbody >
<tr >
<td >RaspberryPi, Type B</td>
<td >$65</td>
</tr>
<tr >
<td >Micro-SD Card, 8GB, Class 10 (with regular SD card adaptor)</td>
<td >$21</td>
</tr>
<tr >
<td >USB Wi-Fi Module, N</td>
<td >$30</td>
</tr>
<tr >
<td >Solid-state Relay D4825</td>
<td >$16</td>
</tr>
<tr>
<td>Electric Blanket</td>
<td>?</td>
</tr>
<tr>
<td>RaspberryPi Prototyping PCB, Adafruit</td>
<td>$30</td>
</tr>
<tr>
<td>240VAC-12VDC Buck Converter</td>
<td>$18</td>
</tr>
<tr>
  <td>12V-to-5V Regulator</td>
  <td>$2.50</td>
</tr>
<tr>
  <td><b>TOTAL</b></td>
  <td>$182.50</td>
</tr>
</tbody>
</table>

## RaspberryPi Setup

I needed a later version of nodejs than sudo apt-get install nodejs would offer, so I downloaded the node v0.11.6 binary from [http://nodejs.org/dist/v0.11.6/](http://nodejs.org/dist/v0.11.6/).

I ran out of room with the standard Raspian image on my harddrive. Used the option in raspi-config to expand the partition to the full SD card size.

I got some weird `cb() never called!` errors when trying to install express with `npm install express`. `npm cache clear` seemed to fix it.

I installed geany (`sudo apt-get install geany`), to get a better code editor than `nano` or `leafpad`.

{{< img src="raspberry-pi-with-lots-of-cables-filtered.jpg" caption="The RaspberryPi while testing."  width="800px" >}}


## List Of Installed Programs

* node
* express (node extension)
* ddclient - Manager for dynamic DNS service

## Controlling GPIO

The `ENOENT read /sys/class/gpio/gpio4/direction` error caught me out for along time, until I realised I had to run the node module using `sudo node server.js` (with administrator privlages).

{{< img src="simple-led-connected-to-raspberry-pi-gpio.jpg" caption="I used a single LED connected up to one of the RaspberryPi's GPIO pins for basic testing."  width="800px" >}}

## Nodejs Modules

Express allows you to easily set up a web server using node.js.

Managed to get the RaspberryPi to take action when the client visited a specific URL.

Wanted to send information back to the server without the client browsing to a different page.

{{< img src="node-js-server-running-on-raspberry-pi-terminal-output-filtered.jpg" caption="The terminal output when a client visits the node.js server running on the RaspberryPi."  width="600px" >}}

The express extension serves up a web page.

{{< img src="basic-web-page-served-by-node-js.jpg" caption="The basic web page served with node.js running on the RaspberryPi (viewed in Chrome)."  width="800px" >}}

At first I was just using the `window.redirect()` to send data back to the server when the user toggled the on/off button. This had the problem of the web page wanting to change everytime you clicked the button. To send back data without reloading the page, I use the AJAX (this was new to me) post request that comes with jQuery, `$.post()`.

The server checks to see if it can resolve the address www.google.com every 5 seconds. If it can, it turns the online LED on, if it can't, it turns it off. This gives the user a good indication of whether the device is connected to the internet or not.

## Using Rsync To Write Code On PC, Then Transfer To RaspberryPi

I discovered rsync was one of the best ways of enabling me write code on my Windows computer, and then transfer it to the RaspberryPi quickly and easily for running.

I used the following command when currently in the repo directory on my PC (note the `.` after `--delete` ,this is important!):

```sh
rsync -arvz --delete . pi@192.168.1.51:~/autoeb
```

{{< img src="sending-files-via-rsync-between-pc-and-raspberry-pi.png" caption="Sending code files using rsync from the PC to the RaspberryPi."  width="800px" >}}

## Dynamic DNS

I used this awesome and simple guide, [http://blog.mivia.dk/2013/03/free-dynamic-dns-for-raspberry-pi/](http://blog.mivia.dk/2013/03/free-dynamic-dns-for-raspberry-pi/)

ddclient

You can reconfigure ddclient with the command dpkg-reconfigure ddclient. You can print out found internet addresses using the command ddclient --query.

The fixed name I gave the RaspberryPi was aeb.flashserv.net.

I gave the RaspberryPi a fixed internal address by configuring settings on the router for "DHCP Reservations". I used the internal address 192.168.1.51.

[Pagekite](https://pagekite.net/) looks interesting, as it means you don't have to setup port forwarding on the router, although I didn't use the service for this project. They have a pay-what-you-want pricing plan, with the basic service being free.

## Automatic Run On Start-up

We want the RaspberryPi server to automatically run on start-up. To do this, I edited some configuration files to make the RaspberryPi automatically login at turn on, and then set it up so a script ran automatically whenever that user logged in, hence it would run at start-up.

This guide is easy to follow...[http://raspberrypi.stackexchange.com/questions/8734/execute-script-on-start-up](http://raspberrypi.stackexchange.com/questions/8734/execute-script-on-start-up) and so is this. [http://www.akeric.com/blog/?p=1976](http://www.akeric.com/blog/?p=1976).

## Forwarding Ports

I set up port forwarding on the router for port 8000. This worked fine for a Vodafone router, however, when I tried to set up the same port forwarding on an Orcon router, it complained that the port 8000 was already in use by something called a "USB Server". I had to change all references of the port to 8001, which meant changing both the node server code and the Android app code.

## Fixed IP

To do this I first had to setup the RaspberryPi so it has a fixed IP. Depending on the router, I could do this one of two ways:

1. Set up a fixed IP purely on the router, using the RaspberryPi's MAC address. This is the easy way!
2. Set up a fixed IP on the RaspberryPi. This is harder!

To make the RaspberryPi request a fixed IP (option 2), you have to modify it's network interface settings.

The file /etc/network/interfaces contains a list of the present network adaptors and their basic settings.

```sh
iface wlan0 inet manual
```

There were many tutorials online on how to modify this file. However, most of them didn't seem to work in my case. The one that did ([http://kerneldriver.wordpress.com/2012/10/21/configuring-wpa2-using-wpa_supplicant-on-the-raspberry-pi/](http://kerneldriver.wordpress.com/2012/10/21/configuring-wpa2-using-wpa_supplicant-on-the-raspberry-pi/)) was when I changed it to:

```sh
# allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet static
    address 10.1.2.20
    netmask 255.255.255.0
    network 10.1.2.0
    gateway 10.1.2.1
```

However, this would not work automatically on start-up. I had to also type the command `sudo ifup wlan0` before the internet would start working.

This would give me the errors:

```sh
ioctl[SIOCSIWAP]: Operation not permitted
ioctl[SIOCSIWENCODEEXT]: Invalid argument
ioctl[SIOCSIWENCODEEXT]: Invalid argument
```

But it still seemed to work fine.

## The Electric Blanket Wiring

I pulled apart the electric blanket. Simple control. Looks like switch selects different resistance circuits to power.

{{< img src="camerazoom-20131009175933171.jpg" caption="The circuit inside the electric blanket controls (for one side of the bed)."  width="800px" >}}

The Pololu ([http://www.pololu.com/catalog/product/2120](http://www.pololu.com/catalog/product/2120)) wasn't enough to power the RaspberryPi with the WiFi module installed (it got hot and then kept restarting).

Maybe a 12V to 5V cigarette lighter USB power port will work?

The solid-state relay didn't have a decent datasheet, although what looks like an exact replica was found ([http://nz.mouser.com/ProductDetail/Crydom/D4825/?qs=sGAEpiMZZMtq49AUx5G3778uEJUSSwFqduP38LjrRb0%3d](http://nz.mouser.com/ProductDetail/Crydom/D4825/?qs=sGAEpiMZZMtq49AUx5G3778uEJUSSwFqduP38LjrRb0%3d)). It shares the same code, D4825.

Although I should of been able to just drive the relay directly from a RaspberryPi GPIO, I choose to use a MOSFET to instead switch it to the +5V rail. I used a TO-92 package (cause it was easy to solder to the prototyping board) BS170"D27Z N-Channel MOSFET.

The switch has a 1kR resistor in series and a 50kR resistor pulling the GPIO pin to ground. The 1kR is to stop any damaging currents if the GPIO pin is accidentally turned into an output.

I had an issue with a energy-saving light flickering about once per second when the relay was not meant to be turned on.

Measured wire resistances:

<table>
  <tbody>
    <tr>
      <td>Brown-Blue</td>
      <td>870Ω</td>
    </tr>
    <tr>
      <td>White-Black</td>
      <td>1.8kΩ</td>
    </tr>
  </tbody>
</table>

How I think the circuit worked:

<table>
  <thead>
    <tr>
      <th>Power Setting</th>
      <th>Connection</th>
      <th>Calculated Power</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>none</td>
      <td>0W</td>
    </tr>
    <tr>
      <td>1</td>
      <td>White-Black 1/2 Cycle</td>
      <td>16W</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Brown-Blue 1/2 Cycle</td>
      <td>33W</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Brown-Blue Full Cycle</td>
      <td>66W</td>
    </tr>
  </tbody>
</table>

## The Android App

I had never developed an Android app before, so the first task was downloading and installing the [Android SDK](http://developer.android.com/sdk/index.html).

The idea was to basically recreate how the web page looked and acted with an Android app. I considered just making an app which loaded the web page, since you have to be connected to the internet to control it anyway.

A thing that caught me out is that the WebView URL has to have `http://` at the front to work, you can't use shortened versions like `www.google.com`.

## Image Gallery

{{< gallery dir="images/project-autoelectricblanket" />}}
