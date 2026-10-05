# 03 · Kinematics Foundations

## Scope

Build a small but complete kinematic model of a planar robot arm. Start with coordinate frames, compute tool pose from joint angles, and then solve the reverse problem.

The examples assume rigid links, ideal revolute joints, a fixed base, and a tool point at the second link's tip.

## Learning objectives

- Express a point in a named coordinate frame.
- Combine a planar rotation and translation.
- Derive and evaluate forward kinematics for a two-link arm.
- Find the inverse kinematics branches for a reachable target.
- Check a solution by substituting it into the forward model.
- Explain why a kinematic solution is not a complete motion plan.
- Derive the planar position Jacobian and identify its singular configurations.

## Prerequisites

[Manipulators and motion](../02-manipulators-and-motion/README.md), basic algebra, the Pythagorean theorem, sine and cosine, and introductory matrix multiplication. The first lesson gives the matrix-vector multiplication used here. The velocity lesson introduces time derivatives and the chain rule used in its derivation. Python is optional.

## Recommended order

1. [Coordinate frames and planar transformations](01-coordinate-frames.md)
2. [Forward kinematics of a planar arm](02-forward-kinematics.md)
3. [Inverse kinematics of a planar arm](03-inverse-kinematics.md)
4. [Velocity kinematics and the Jacobian](04-velocity-kinematics.md)
5. [Jacobians and singularities](05-jacobians-and-singularities.md)
6. [Exercises](exercises.md), then [worked solutions](solutions.md)

To extend these models to three dimensions, continue with [spatial kinematics](../07-spatial-kinematics/README.md): rotation representations, homogeneous transforms, and standard DH. It can be read before the control section.

[Course index](../README.md) · [Next section: Control and interaction](../04-control-and-interaction/README.md)
