---
title: Quaternion
date: 2024-04-06
---


### Quaternion

A quaternion is a type of hypercomplex number that extends complex numbers. It is typically represented as:

$$q = a + bi + cj + dk$$

where:
- $a$, $b$, $c$, and $d$ are real numbers,
- $i$, $j$, and $k$ are the fundamental quaternion units.

Quaternions have properties that make them useful for representing rotations and orientations in three-dimensional space. They avoid the singularity and ambiguity problems of Euler angles and are more compact than rotation matrices.

WATCH THIS: https://eater.net/quaternions

### Operations with Quaternions

Quaternions support addition, subtraction, multiplication, and division, but multiplication is not commutative:

$$ij = k, \quad ji = -k, \quad jk = i, \quad kj = -i, \quad ki = j, \quad ik = -j, \quad i^2 = j^2 = k^2 = ijk = -1$$

### Quaternion Conjugate

The conjugate of a quaternion $q = a + bi + cj + dk$ is defined as:

$$q^* = a - bi - cj - dk$$

### Norm of a Quaternion

The norm of a quaternion is given by:

$$\|q\| = \sqrt{a^2 + b^2 + c^2 + d^2}$$

### Quaternion Inverse

The inverse of a quaternion $q$ is defined as:

$$q^{-1} = \frac{q^*}{\|q\|^2}$$

### Quaternion Matrix

A quaternion matrix is a matrix where each element is a quaternion. These matrices can represent complex transformations in higher-dimensional spaces and are used in various fields, including theoretical physics, computer graphics, and robotics.



### Applications

Quaternion matrices are particularly useful for:
- Rotating points in three-dimensional space,
- Interpolating orientations (slerp),
- Simulating rigid body dynamics.

Their ability to represent rotations without suffering from gimbal lock makes them invaluable in 3D computer graphics and aerospace engineering.
