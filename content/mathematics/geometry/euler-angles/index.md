---
authors: [ "Geoffrey Hunter" ]
date: 2019-02-20
draft: false
lastmod: 2019-02-20
tags: [ "matrix", "rotation", "complex", "interpolation", "Euler", "angle", "RPY", "gimbal lock", "attitude", "orientation", "vector", "intrinsic", extrinsic" ]
title: "Euler Angles"
type: page
---

## Overview

Euler angles is a way of describing the rotation in 3D space using three separate rotations around an axes.

{{% note %}}
Euler's theorem states that the rotation of a rigid body can be described by a single rotation about a single axis.
{{% /note %}}


## Syntax

Euler angles are usually defined one of the two symbol sets:

* `\( \alpha, \beta, \gamma \)` (Alpha, Beta, Gamma). These are usually used with _proper Euler angles_ (see below).
* `\( \Phi, \Theta, \Psi \)` (Phi, Theta, Psi). These are usually used with _Tait-Bryan angles_ (see below).


## Proper Euler Angles vs. Tait-Bryan Angles

Euler angles can be split into two categories based on the axis used:

* **Proper Euler Angles**: These use the same axis for both the first and third rotations, e.g. x-y-x, x-z-x, y-x-y, y-z-y, z-x-z, z-y-z
* **Tait-Bryan Angles**: These use all three axis (no axis is used twice), e.g. x-y-z, x-z-y, y-x-z, y-z-x, z-x-y, z-y-x

Proper Euler angles are also called **classic Euler angles**.

The classic roll, pitch, yaw (RPY) terminology is a Tait-Bryan angle. Tait-Bryan angles are also called **Cardan angles**, **nautical angles**, or **heading, elevation and bank**.

The axes of the initial frame (also called the reference frame) is denoted with x, y, z. The rotated frame is denoted with X, Y, Z.

The line of nodes is the line (or vector) made by the intersection of the xy and XY planes.


## Calculating Euler Angles Between Two 3D Vectors

First we calculate the cross-product of the two vectors, which gives us the vector of rotation:

<div>$$ \mathbf{N} = \mathbf{a} \times \mathbf{b} $$</div>

<div>$$ \cos{\theta} = \frac{a \cdot b}{length(a)*length(b)} $$</div>

If you are using unit vectors, you can ignore the lengths (this would just divide by 1).


## Conversion To Rotation Matrices

Euler angles can be converted to rotation matrices.

<div>$$
\mathbf{R_x(\gamma)} = \begin{bmatrix}
    1 &     0 &             0 \\
    0 &     \cos{\gamma} &  -\sin{\gamma} \\
    0 &     \sin{\gamma} &  \cos{\gamma}
\end{bmatrix}
$$</div>


<div>$$
\mathbf{R_y(\beta)} = \begin{bmatrix}
    \cos{\beta} &   0 &     \sin{\beta} \\
    0 &             1 &     0 \\
    -\sin{\beta} &  0 &     \cos{\beta}
\end{bmatrix}
$$</div>

<div>$$
\mathbf{R_z(\alpha)} = \begin{bmatrix}
    \cos{\alpha} &  -\sin{\alpha} &     0 \\
    \sin{\alpha} &  \cos{\alpha} &      0 \\
    0 &             0 &                 1     
\end{bmatrix}
$$</div>

We can combine these to form a single rotation matrix:

<div>$$ \mathbf{R(\alpha, \beta, \gamma)} = \mathbf{R_z(\alpha)} \mathbf{R_y(\beta)} \mathbf{R_x(\gamma)} $$</div

Remember that these a proper matrix multiplications! This order performs the roll, then the pitch, then the yaw. These are extrinsic rotations?

Once the rotation matrix has been calculated, you can rotate any point/vector in the original reference frame to the rotated frame with the equation:

<div>$$
\begin{bmatrix}x_1 \\ y_1 \\ z_1\end{bmatrix} =
\mathbf{R} \begin{bmatrix}x_0 \\ y_0 \\ z_0\end{bmatrix} 
$$</div>


## Conversion From Rotation Matrices

<div>$$
\alpha = atan2{r_{32}, r_{33}} \\
\beta = -a \sin{r_{31}} \\
\gamma = atan2{r_{21}, r_{11}}
 $$</div>

 where `\( atan2(y, x) \)` returns the **principle angle**.

 