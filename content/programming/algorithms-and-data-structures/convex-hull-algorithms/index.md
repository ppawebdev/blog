---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Algorithms" ]
date: 2019-06-17
description: "A tutorial on popular convex hull algorithms."
draft: false
lastmod: 2019-06-19
tags: [ "programming", "algorithms", "convex hull", "Jarvis March", "gift wrapping algorithm", "scipy", "shapely" ]
title: "Convex Hull Algorithms"
type: "page"
---

## Overview

Given a cloud of points on a 2D plane, a convex hull is the smallest set of points which encloses all of the points.

{{% img src="convex_hull.png" width="700px" caption="The 2D convex hull for a set of points." %}}

Another useful concept related to convex hulls is the _minimum bounded rectangle_. The minimum bounded rectangle is the smallest rectangle (measured by area) which encompasses the entire convex hull (by extension, it is also the smallest rectangle that encompasses all points).

The minimum bounded rectangle must have an edge which is co-linear to one of the edges in the convex hull.

## The Jarvis March (Gift Wrapping Algorithm)

Orientation:

<p>$$ o = (q_y - p_y)(r_x - q_x) - (q_x - p_x)(r_y - q_y) $$</p>

* If `\(o == 0\)` they are co-linear
* If `\(o > 0\)` they are clockwise
* If `\(o < 0\)` they are counter-clockwise

This equation comes from the 3D definition of the cross-product (for a proof, see [here](https://stackoverflow.com/questions/17592800/how-to-find-the-orientation-of-three-points-in-a-two-dimensional-space-given-coo)).

1. Pick one point that is guaranteed to lie in the convex hull. This can be done by picking the left-most point (i.e. has the lowest x value). If there is more than one point that meets this condition, you are free to choose any one. Add this to the start of list of the `convex_hull` points.
1. Pick any other point to be the potential `next_point` on the hull.
1. Iterate over all the points, checking the orientation between the `last_point` found on the hull, the potential `next_point`, and the `loop_point` you are currently iterating over. If the orientation is counter-clockwise, then `loop_point` is to the left the the line formed by between `last_point` and `next_point`, and becomes the `next_point`.
1. One you reach the end of the loop, `next_point` is guaranteed to be the correct next point on the convex hull. Append this to the `convex_hull` list.
1. Repeat steps 2 to 4, until you end up adding the same point to the `convex_hull` list as you started with (the left most point).
1. Done!

## Scipy

scipy provides a `ConvexHull` object which can be used to calculate a convex hull from a set of points.

## Shapely

The Shapely library for Python has built-in support for finding the minimum bounded rectangle for a generic geometry type. Shapely can find the minimum bouded rectangle for polygons, point sequences, e.t.c.

```py
BaseGeometry.minimum_rotated_rectangle()
```

```py

Polygon([
  [1, 1],
  [2, 1],
  [5, 4],
  [4, 3],
  [6, 2],
])
```

## Other Resources

[https://www.geometrictools.com/Source/ComputationalGeometry.html](https://www.geometrictools.com/Source/ComputationalGeometry.html) contains some useful geometric algorithms for C/C++, including convex hull algorithms and code for finding the minimum bounding box/volume/circle/sphere e.t.c.

[https://stackoverflow.com/questions/13542855/python-help-to-implement-an-algorithm-to-find-the-minimum-area-rectangle-for-gi](https://stackoverflow.com/questions/13542855/python-help-to-implement-an-algorithm-to-find-the-minimum-area-rectangle-for-gi) contains useful information to fin the minimum bounded rectangle.

[https://www.geometrictools.com/Documentation/MinimumAreaRectangle.pdf](https://www.geometrictools.com/Documentation/MinimumAreaRectangle.pdf) is a very detailed and precies explanation on how the minimum bounded rectangle algorithm works. See [here](2015-05-17-DavidEberly-MinimumAreaRectangle.pdf) for a cached copy.