---
authors: [ "Geoffrey Hunter" ]
date: 2017-10-23
draft: false
lastmod: 2017-10-23
title: "Coordinate Conversion"
type: "page"
---

## Haversine Formula

The _Haversine_ formula can be used to find the shortest distance (great circle distance) between two points on the earth's surface, given their latitude and longitude coordinates.

<div>$$ d = 2r \cdot arcsin(\sqrt{sin^2(\frac{\varphi_2 - \varphi_1}{2}) + cos(\varphi_1)cos(\varphi_2)sin^2(\frac{\lambda_2 - \lambda_1}{2})}) $$</div>

<p class="centered">
    where:<br>
    \( d \) is the shortest (great circle) distance between the two points, in meters<br>
    \( r \) radius of the earth, in meters *(see below)<br>
    \( \varphi_1, \lambda_1 \) is the latitude and longitude of point 1, in radians<br>
    \( \varphi_2, \lambda_2 \) is the latitude and longitude of point 2, in radians<br>
 </p>

The typical value used for `\( r \)` is `\( 6731 \times 10^3 m \)`, which is the mean radius of the earth.

The code for this formula in many different languages can be found at [https://rosettacode.org/wiki/Haversine_formula](https://rosettacode.org/wiki/Haversine_formula).

You may also see this Haversine distance formula written as:

<div>$$ 
    a = sin^{2}(\frac{\varphi_2 - \varphi_1}{2}) + cos(\varphi_1) \cdot cos(\varphi_2) \cdot sin^{2}(\frac{\lambda_2 - \lambda_1}{2}) \\  
    c = 2 \cdot atan2(\sqrt{a}, \sqrt{1 - a}) \\
    d = r \cdot c 
$$</div>

where all the symbols have the same meaning as above

These two formulas are equivalent!

## Bearing

This formula calculates the initial bearing, given a start and end co-ordinate.

<div>$$ \theta = atan2(sin(\lambda_2 - \lambda_1) \cdot cos \varphi_2 \cdot cos \varphi_1 \cdot sin \varphi_2 - \\  
 sin \varphi_1 \cdot cos \varphi_2 \cdot cos(\lambda_2 - \lambda_1)) $$</div>

<p class="centered">
    where:<br>
    \( \theta \) is the initial bearing, in radians, from \( -\pi \) to \( +\pi \)<br>
    \( \varphi_1, \lambda_1 \) is the latitude and longitude of point 1, in radians<br>
    \( \varphi_2, \lambda_2 \) is the latitude and longitude of point 2, in radians<br>
</p>

Note that this calculates the _initial bearing_, which is the bearing you would have to be pointing in at the first co-ordinate to travel to the second co-ordinate along a great circle (shortest path on the sphere). **As you travel there, the bearing is likely to change** (there are a few cases in where it wouldn't change, one being if you were travelling exactly North).

## Destination Coordinate Given Distance And Bearing From Start Coordinate

The following formula allows you to calculate a destination coordinate (lat/lon) if you know a starting coordinate (again, in lat/lon), ground distance (great circle distance) and initial bearing.

<div>$$ \delta = \frac{d}{R} \\  
 p_{2,lat} = \arcsin(\sin p_{1,lat} \cdot \cos \delta + \cos p_{1,lat} \cdot \sin \delta \cdot \cos \theta ) \\  
 p_{2,lon} = p_{1,lon} + \arctan2(\sin \theta \cdot sin \delta \cdot \cos p_{1,lat}, \cos \delta - \sin p_{1,lat} \cdot \sin p_{2,lat}) $$</div>

<p class="centered">
    where:<br>
    \(\delta\) = angular distance, in radians<br>
    \(d\) = ground (great circle) distance between start coordinate and destination coordinate, in meters<br>
    \(R\) = radius of the earth, in meters \( (6871 \times 10^3m) \)<br>
    \(\theta\) = initial bearing from start to destination coordinate (clockwise from North), measured in radians<br>
    \(p_1\) = starting coordinate, latitude and longitude measured in radians<br>
 \(p_2\) = destination coordinate, latitude and longitude measured in radians<br>
 </p>

Note that `\( p_{2,lon} \)` depends on `\( p_{2,lat} \)`, so you have to calculate the latitude of p2 before you can calculate the longitude.
