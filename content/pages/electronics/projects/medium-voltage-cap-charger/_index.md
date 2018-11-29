---
author: gbmhunter
date: 2012-07-24 05:43:55+00:00
draft: false
title: Medium-Voltage Cap Charger
type: page
url: /electronics/projects/medium-voltage-cap-charger
---

Project Start Date: March 2006
Project End Date: April 2006
Current State: Completed

**The Crucial Stats:**
Input Voltage: 12V
Maximum Charge Voltage: 500V

This was before I knew what a boost converter was, so I used the Aahz's Boost Converter  design (member of the www.4hv.org forum). A blurry schematic (the only one I have!) of his design is shown below.

{{< figure src="/images/electronics-mediumvoltagecapcharger/aahzs-boost-converter-schematic.jpg" caption=""  width="400px" >}}

The only thing I would do differently would be to improve the MOSFET switching, as it gets very hot during use. Something is causing the MOSFET to remain in it's linear region for too long.