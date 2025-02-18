---
authors: [ "Geoffrey Hunter" ]
categories: [ "Electronics", "PCB Design", "Component Packages" ]
date: 2015-04-05
draft: false
tags: [ "component packages", "PCB design", "Mini DIP", "BLDC", "motors", "dual in-line package" ]
title: Mini-DIP SPM
type: page
---

## Overview

<table>
<tbody>
<tr>
<td >Name</td>
<td >Mini Dual In-Line Package
</td>
</tr>
<tr >
<td >Synonyms</td>
<td>
  <ul>
    <li>SPM27-JA</li>
    <li>SPM27-CC</li>
    <li>SPM27-EC</li>
  </ul>
</td>
</tr>
<tr >
<td >Variants</td>
<td >n/a</td>
</tr>
<tr>
  <td>Similar To</td>
  <td>{{% link text="DIP" src="../dip-component-package" %}}</td>
</tr>
<tr>
<td>Mounting</td>
<td>TH</td>
</tr>
<tr>
<td>Pin Count</td>
<td>27</td>
</tr>
<tr>
<td>Pitch</td>
<td >1.778mm, 2.050mm, 2.531mm (3 different pitches on the one package!)</td>
</tr>
<tr >
<td >Solderability</td>
<td >Easy to solder by hand.</td>
</tr>
<tr >
<td >Thermal Resistance</td>
<td >n/a</td>
</tr>
<tr >
<td >Land Area</td>
<td >Mini-DIP SPM 27 : 44mm x 26.8mm = 1179.2mm^2</td>
</tr>
<tr >
<td >Height</td>
<td >3.15mm (when mounted)</td>
</tr>
<tr >
<td >3D Models</td>
<td >n/a</td>
</tr>
<tr>
<td >Common Uses</td>
<td>BLDC motor drivers from Fairchild</td>
</tr>
</tbody>
</table>

## Comments

The SPM27-JA does not have a top-side copper face, while the SPM27-CC and SPM27-EC do. The copper face has been designed specifically for heatsinking as these ICs are designed to be able to handle plenty of power. This package is rather unique in the fact it contains a three-phase IGBT inverter circuit power block and four drive ICs. As of 2012, only a 27-pin variant exists.

## 3D Renders

{{< img src="mini-dip-spm-component-package-3d-render.png" width="412px" caption="A 3D render of the Mini-DIP SPM component package."  >}}