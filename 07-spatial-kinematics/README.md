# 07 · Spatial Kinematics

## Scope

Extend planar kinematics to three-dimensional position and orientation. Learn how to describe rotations, convert between orientation representations, combine rigid transformations, and build a serial-arm model using standard Denavit–Hartenberg (DH) parameters.

A free rigid body has three translational and three rotational degrees of freedom. A particular robot may control fewer: representing its tool with a six-dimensional pose does not give its mechanism six independent motions.

## Learning objectives

- Interpret a rotation matrix as the axes of one frame expressed in another.
- Distinguish rotating a vector from changing its coordinates.
- Compose rotations about fixed and moving axes in the correct order.
- Convert between rotation matrices, roll–pitch–yaw, proper Euler angles, axis–angle, and unit quaternions.
- Recognize orientation-coordinate singularities and nonunique representations.
- Transform points and free vectors correctly using homogeneous coordinates.
- Assemble forward kinematics from standard DH transforms and fixed base/tool offsets.

## Prerequisites and conventions

Read [kinematics foundations](../03-kinematics-foundations/README.md) first. This section can follow Section 03 directly; Sections 04–06 are not prerequisites. You will use matrix multiplication, transpose, dot products, and cross products.

All frames are right-handed. Coordinates are column vectors. ${}^{A}R_B$ maps coordinates from frame $B$ into frame $A$. Positive rotations follow the right-hand rule. Equations use radians; numerical examples marked with $^\circ$ use degrees. Quaternions are scalar-last with Hamilton multiplication. DH parameters use the standard convention stated in Lesson 08.

## Recommended order

1. [Points, vectors, and rotation matrices](01-rotation-matrices.md)
2. [Rotation order and frame changes](02-rotation-composition.md)
3. [Roll, pitch, and yaw](03-roll-pitch-yaw.md)
4. [Proper Euler angles](04-euler-angles.md)
5. [Axis–angle and exponential coordinates](05-axis-angle.md)
6. [Unit quaternions](06-unit-quaternions.md)
7. [Spatial homogeneous transformations](07-homogeneous-transformations.md)
8. [Standard DH and forward kinematics](08-denavit-hartenberg.md)
9. [Exercises](exercises.md), then [worked solutions](solutions.md)

[Course index](../README.md) · [Planar foundation](../03-kinematics-foundations/README.md)
