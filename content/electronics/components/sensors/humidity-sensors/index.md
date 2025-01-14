---
authors: [ "Geoffrey Hunter" ]
date: 2016-02-04
draft: false
title: Humidity Sensors
type: page
---

## Types

Humidity sensors can either contain just the humidity sensing component (which means they usually just have two leads), or they may also contain signal processing circuits. The ones which also contain circuitry have an analogue (usually 3 pin) or digital output (can have many pins, 8 is a common number).

## Uses

Humidity sensors are commonly used in the following equipment:

* Air conditioning, heating and ventilation
* Refrigerators
* Industrial automation
* Asset and goods tracking
* Medical equipment (respiratory devices)

## Relative Humidity

Relative humidity is defined as the ratio of the water vapour pressure to the saturation water vapour pressure, at the current gas temperature.

It is ratio of the actual amount of water in the air to the total amount it could when saturated.

<p>$$ RH = \frac{P_W}{P_{WS}}\cdot 100% $$</p>

## Dew Point

The _dew point_ is the point at which the atmosphere has to be **cooled down** too so that **condensation** starts to appear. The frost point is the dew point when the temperatures are below freezing.

## The Magnus Equation

The Magnus equation is an approximation to calculate the dew point from the actual air temperature and relative humidity. It is a useful equation to use when you have a sensor IC which measures both temperature and relative humidity.

First we find an intermediary value called gamma (`\(\gamma\)`):

<div>$$ \gamma(T, RH) = ln(\frac{RH}{100}) + \frac{bT}{c + T} $$</div>

<p class="centered">
    where:<br>
    \(RH\) = relative humidity of the air (as a percentage from 0-100%)<br>
    \(T\) = temperature of air, in degrees Celsius<br>
    \(b\) = constant<br>
    \(c\) = constant<br>
</p>

`\(\gamma\)` can then be substituted into the following equation to calculate the dew point temperature `\(T_{dp}\)` (in degrees Celsius):

<div>$$ T_{dp} = \frac{c\gamma(T, RH)}{b - \gamma(T, RH)} $$</div>

The values of the constants `\(a\)`, `\(b\)` and `\(c\)` can vary depending on the data set and method used to calculate them (this is an empirical formula). Common values for them are:

`\(a = 6.112millibar\)`
`\(b = 17.67\)`
`\(c = 243.5^{\circ}C\)`

The following is a code example in C showing a function which converts temperature and relative humidity into a dew point, using the simple Magnus equation.

```c
#include <math.h>

//! @brief		The B constant for the Magnus equation to calculate the dew point.
#define DEW_POINT_CONSTANT_B_NO_UNIT	17.67

//! @brief		The C constant for the Magnus equation to calculate the dew point.
#define DEW_POINT_CONSTANT_C_DEG_C		243.5

//! @brief		Calculates the dew point (in degrees Celcius) from the temperature and relative humidity.
//! @details 	Uses the Magnus formula, given at https://en.wikipedia.org/wiki/Dew_point.
//! @param		temperature_DegC 		The temperature of the atmosphere at which the relative humidity was measured.
//! @param		relHumidity_Perc 		The relative humidity (as a percentage from 0-100) of the atmosphere measured.
//! @returns 	The dew point (in degrees Celcius) of the atmosphere.
double Humidity_CalcDewPointDegC(double temperature_DegC, double relHumidity_Perc) {
  
  // This uses the Magnus equation as explained at https://en.wikipedia.org/wiki/Dew_point
  
  // Calculate gamma, which is just a way of splitting up the equation into two operations
  double gamma = log(relHumidity_Perc/100.0) + (DEW_POINT_CONSTANT_B_NO_UNIT*temperature_DegC)/(DEW_POINT_CONSTANT_C_DEG_C + temperature_DegC);
  
  // Finally, calculate the dew point (in degrees Celcius)
  double dewPoint_DegC = (DEW_POINT_CONSTANT_C_DEG_C*gamma)/(DEW_POINT_CONSTANT_B_NO_UNIT - gamma);
  
  return dewPoint_DegC;
  
}
```

## Examples

The Honeywell HIH-5030 (3.3V) or HIH-4030 (5.0V) analogue-output, 3-pin, SMD humidity sensors are a popular choice. They measure the full humidity range (0-100%), are easy to solder, and simple to interface too.
