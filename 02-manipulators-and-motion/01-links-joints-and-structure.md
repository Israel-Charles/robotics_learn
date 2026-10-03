# Links, Joints, and Robot Structure

## Build a chain from the base to the tool

A **link** is a body in a mechanism, often treated as rigid in introductory models. A **joint** connects bodies and permits specified relative motion. The **base** anchors the chain or attaches it to another platform. The **end effector** performs the task at the working end.

A simple serial arm can be represented as:

```text
base — joint 1 — link 1 — joint 2 — link 2 — tool
```

A serial chain has one sequence of links and joints from base to tool. A parallel mechanism connects its moving platform to its base through multiple chains, creating closed loops. Those loops constrain motion, so counting joints alone does not determine mobility.

## Common ideal joint models

| Joint | Permitted relative motion | Ideal joint DOF | Coordinate |
| --- | --- | --- | --- |
| Revolute, R | Rotation about one fixed joint axis | 1 | Angle, in rad |
| Prismatic, P | Translation along one fixed joint axis | 1 | Displacement, in m |
| Spherical | Rotation about a common center in three dimensions | 3 | Three local orientation coordinates |
| Fixed | No relative motion | 0 | None |

A joint's ideal degrees of freedom do not state its number of actuators. Some permitted motions may be passive. Real joints also have travel limits, friction, compliance, and clearance that ideal models omit.

### Coupled motion: a screw example

Imagine a screw turning through a fixed nut. Suppose its **lead** is 2 mm per revolution: one complete turn advances the screw 2 mm along its axis. The angular and linear motions are linked:

$$
d=\frac{\ell}{2\pi}\theta,
$$

where $\ell$ is the lead, $\theta$ is rotation in radians from the chosen zero, and $d$ is axial displacement from that zero. For half a turn, $\theta=\pi$ rad:

$$
d=\frac{2\text{ mm}}{2\pi}\pi=1\text{ mm}.
$$

You cannot choose the rotation and displacement separately while the screw remains engaged with the fixed nut. Specifying either one determines the other, so this ideal screw joint has **one DOF**, even though it both rotates and translates.

### Closed loops: linked joints do not move independently

Consider four rigid bars connected into a planar quadrilateral, with the bottom bar fixed to the ground. Four pin joints allow relative rotation, but all bars must remain connected:

```text
       B o--------o C
        /          \
       /            \
    A o==============o D
           fixed base
```

At an ordinary configuration of a movable four-bar linkage, choosing the angle of bar AB determines the other bar angles locally, on the selected assembly branch. You cannot choose all four pin angles independently: arbitrary choices would pull a connection apart. Such a linkage generally has one independent motion, not four. Special geometries or singular configurations need separate analysis.

## Common manipulator arrangements

| Arrangement | Typical positioning structure | Useful intuition |
| --- | --- | --- |
| Cartesian | Three orthogonal prismatic joints | Moves along three linear axes |
| Cylindrical | A rotation and two translations | Sweeps around a base axis while changing radius and height |
| Articulated | Several revolute joints | Bends through shoulder-like and elbow-like motions |
| SCARA | Commonly two parallel revolute positioning joints, vertical travel, and tool rotation | Suited to many planar transfer and insertion tasks |
| Parallel | Multiple chains support a platform | Motion is constrained by all chains together |

Additional wrist or tool joints can change these arrangements' capabilities. A family name does not specify every joint or workspace limit.

## Interpreting a six-axis arm

A common industrial arm uses six revolute joints. The first joints position the arm, while later joints help orient the tool. The familiar base, shoulder, elbow, and wrist analogy can help identify parts, but it is not a complete mathematical model.

Joint axes belong to the mechanism and move as upstream links move. They should not automatically be labeled as global roll, pitch, and yaw axes. The geometry and the coordinate-frame convention determine how joint angles contribute to tool orientation.

### The mounting flange and the tool center point

The **mounting flange** is the attachment surface at the end of the arm. The **tool center point (TCP)** is a selected point on the attached tool used to describe its task motion. For a torch, it might be the tip; for a gripper, it might be the center of the grasp between its fingers. It need not be the tool's center of mass or the flange origin.

```text
arm --- [flange origin] -------- 0.15 m -------- [TCP]
```

The robot needs the displacement from flange to TCP to locate the working point. Replacing a short tool with a longer one changes this displacement even if every arm joint stays still.

## Checkpoint

A flange origin is at $(0.40,0.20)$ m in a planar base frame. The TCP is 0.15 m along the flange's local positive $x$ direction. Where is the TCP when the flange points right? What if the flange instead points upward at the same origin?

When it points right, the offset in the base frame is $(0.15,0)$ m:

$$
p_{\mathrm{TCP}}=(0.40,0.20)+(0.15,0)=(0.55,0.20)\text{ m}.
$$

When it points upward, the offset is $(0,0.15)$ m:

$$
p_{\mathrm{TCP}}=(0.40,0.20)+(0,0.15)=(0.40,0.35)\text{ m}.
$$

The flange origin is the same in both cases, but the working point is not. The offset must be expressed in the same frame as the flange position before adding them. [Coordinate frames](../03-kinematics-foundations/01-coordinate-frames.md) develops that operation mathematically.

## Quick reference

- Links describe bodies; joints describe permitted relative motion.
- `R` means revolute; `P` means prismatic.
- Serial and parallel mechanisms have different constraint structures.
- The TCP is a selected task point, not necessarily the last joint or flange origin.

[Section index](README.md) · [Next: Degrees of freedom](02-degrees-of-freedom.md)
