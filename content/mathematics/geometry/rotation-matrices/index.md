---
authors: [ "Geoffrey Hunter" ]
date: 2019-02-25
description: "An introduction to rotation matrices. What they are, how to calculate them, and what they are useful for."
draft: false
lastmod: 2019-11-13
tags: [ "matrix", "interpolation", "angle", "attitude", "orientation", "vector", "rotation", "rotation matrix", "dot product", "reference frame", "coordinate system", "RPY", "Euler angles", "origin", "THREE.js", "determinant", "orthogonal" ]
title: "Rotation Matrices"
type: "page"
---

## Overview

Rotation matrices are matrices which are used to describe the **rotation of a rigid body from one orientation to another**.

In `\(\mathbb{R3}\)` they form a 3x3 matrix.

<p>$$
\mathbf{R} = \begin{bmatrix} \hat{u_x} & \hat{v_x} & \hat{w_x} \\ \hat{u_y} & \hat{v_y} & \hat{w_y} \\ \hat{u_z} & \hat{v_z} & \hat{w_z} \end{bmatrix}
$$</p>

such that if `\(\vec{\b{a}}\)` was a point in 3D space, then we can rotate `\(\vec{\b{a}}\)` to `\(\vec{\b{b}}\)` around the origin by applying `\(\b{R}\)` in the following manner:

<p>$$
\b{R}\vec{\b{a}} = \vec{\b{b}}
$$</p>

<p class="centered">
where:<br>
\(\b{a}\) and \(\b{b}\) are 1x3 vectors<br>
</p>

Rotation matrices are always **orthogonal matrices which have a determinant of 1**.

## Combining Rotations

Two successive rotations represented by `\(\b{R_1}\)` and `\(\b{R_2}\)` can be represented by a single rotation matrix `\(\b{R_3}\)` where:

<p>$$ \b{R_3} = \b{R_2} \b{R_1} $$</p>

Pay careful attention to the order of the matrix multiplication, successive rotation matrices are multiplied on the left.

## How To Find The Rotation Matrix Between Two Coordinate Systems

Suppose I have the frame with the following unit vectors defining the first coordinate system `\( X1Y1Z1 \)`:

<p>$$
X1=\begin{bmatrix}x_x\\x_y\\x_z\end{bmatrix} \quad Y1=\begin{bmatrix}y_x\\y_y\\y_z\end{bmatrix} \quad Z1=\begin{bmatrix}z_x\\z_y\\z_z\end{bmatrix}
$$</p>

And a second coordinate system `\( X2Y2Z2 \)` defined by the unit vectors:

<p>$$
X2=\begin{bmatrix}x_x\\x_y\\x_z\end{bmatrix} \quad Y2=\begin{bmatrix}y_x\\y_y\\y_z\end{bmatrix} \quad Z2=\begin{bmatrix}z_x\\z_y\\z_z\end{bmatrix}
$$</p>

The rotation matrix `\( R \)` which rotates objects from the first coordinate system `\(X1Y1Z1\)` into the second coordinate system `\(X2Y2Z2\)` is:

<p>$$
R = \begin{bmatrix}
  X1 \cdot X2 & X1 \cdot Y2 & X1 \cdot Z2\\
  Y1 \cdot X2 & Y1 \cdot Y2 & Y1 \cdot Z2\\
  Z1 \cdot X2 & Z1 \cdot Y2 & Z1 \cdot Z2\\
\end{bmatrix}
$$</p>

<p class="centered">
  where:<br>
  \( \cdot \) is the matrix dot product<br>
  and everything else as above
</p>

## Creating A Rotation Matrix From Euler Angles (RPY)

A rotation expressed as Euler angles (which includes RPY or roll-pitch-yaw notation) can be easily converted into a rotation matrix. To represent a extrinsic rotation with Euler angles `\( \alpha \)`, `\( \beta \)`, `\( \gamma \)` are about axes `\( x \)`, `\( y\)`, `\( z \)` can be formed with the equation:

<p>$$ \b{R} = \b{R}_z(\gamma) \b{R}_y(\beta) \b{R}_x(\alpha) $$</p>

where:

<p>$$
\b{R}_x(\theta) = \begin{bmatrix}
  1 & 0            & 0             \\
  0 & \cos(\theta) & -\sin(\theta) \\
  0 & \sin(\theta) & \cos(\theta)  \\
\end{bmatrix} \\

\b{R}_y(\theta) = \begin{bmatrix} 
  \cos(\theta)  & 0 & \sin(\theta) \\
  0             & 1 & 0            \\
  -\sin(\theta) & 0 & \cos(\theta) \\
\end{bmatrix} \\

\b{R}_z(\theta) = \begin{bmatrix}
  \cos(\theta) & -\sin(\theta) & 0 \\
  \sin(\theta) & \cos(\theta)  & 0 \\
  0            & 0             & 1
\end{bmatrix}
$$</p>

## Converting A Rotation Matrix To Euler Angles

Whilst converting a rotation expressed as Euler angles is relatively trivial (see above), it is not no simple to go the other way and convert a rotation matrix to Euler angles. 

### Javascript

THREE.js has a `Euler` class with the function `.setFromRotationMatrix()` which can convert a rotation matrix to Euler angles. The supported Euler angle orders are `XYZ`, `YZX`, `ZXY`, `XZY`, `YXZ`, `ZYX`, and it only supports _intrinsic_ rotations.

## External Resources

https://www.andre-gaschler.com/rotationconverter/ is a great one-page rotation calculator.