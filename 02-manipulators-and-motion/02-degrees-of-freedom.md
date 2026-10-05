# Degrees of Freedom and Configuration

## Count independent coordinates

A mechanism's **degrees of freedom (DOF)** are the number of independent coordinates needed to specify its configuration, locally. Coordinates describe the mechanism's arrangement; they are not separate coordinate systems.

For a fixed-base, open serial chain of independent one-DOF joints, the number of joint coordinates equals the number of joints. This simple counting rule does not automatically apply to closed loops, mechanically coupled joints, or more general joint types.

A two-revolute-joint planar arm has the configuration vector

$$
q = \begin{bmatrix}\theta_1 \\ \theta_2\end{bmatrix}.
$$

The elbow angle $\theta_2$ is measured relative to the preceding link. Specifying both angles fixes the arm's configuration under the ideal model.

## Configuration is different from task description

A rigid body moving in a plane has three pose coordinates:

$$
(x, y, \phi),
$$

where $x,y$ specify position and $\phi$ specifies orientation. A freely moving rigid body in three-dimensional space has six pose DOF: three for translation and three for orientation. Six is a count of independent freedoms, not a requirement to use exactly six numbers in every representation; rotation matrices use nine entries subject to constraints.

A two-joint planar arm has only two independently adjustable coordinates. It can generally control its tool's planar position locally, away from singularities, but cannot independently prescribe both position coordinates and orientation. Its orientation follows from its joint angles:

$$
\phi = \theta_1 + \theta_2
$$

This sum assumes that both links point along the base's positive $x$ direction at zero joint angles and that the tool points along link 2. For example, rotating the shoulder $30^\circ$ turns both links by $30^\circ$. Rotating the elbow another $-20^\circ$ relative to link 1 leaves link 2, and the aligned tool, pointing at $10^\circ$ relative to the base.

If a tool is mounted at a fixed angle $\alpha$ relative to link 2, its orientation instead becomes $\phi=\theta_1+\theta_2+\alpha$. The simpler sum uses $\alpha=0$.

### Two adjustment knobs, three requested quantities

Think of the two joint angles as two adjustment knobs. The tool's $x$, $y$, and $\phi$ are the resulting measurements. Turning either knob generally changes several measurements at once. Once the angles have been selected to place the tip at a particular $(x,y)$, there is generally no independent knob left to choose $\phi$ freely.

An extreme example makes this visible: to reach the farthest point $(a_1+a_2,0)$, both links must point right. The aligned tool then points right too. You cannot keep the tip at that farthest point while making the tool point upward using only those two joints.

| What are we describing? | Values needed | Meaning of the count |
| --- | --- | --- |
| The planar 2R arm's configuration | $\theta_1,\theta_2$ | Two independent joint settings |
| A requested planar tool position | $x,y$ | Two target values |
| A requested planar tool pose | $x,y,\phi$ | Three target values, which a 2R arm cannot generally choose independently |
| A free body's spatial pose | Three position and three orientation coordinates, locally | Six independent pose freedoms |

The number of target values describes the task. It does not grant the mechanism that many independent adjustments. Some particular pose targets are achievable; arbitrary combinations of all three planar pose values are not.

## Redundancy depends on the task

A manipulator is kinematically redundant for a task when it has more independent configuration variables than are needed for that task, at a regular configuration. For example, a seven-joint arm can have an extra freedom when performing a six-dimensional tool-pose task. That extra freedom may help avoid obstacles or joint limits.

It does not guarantee a feasible solution for every target. Geometry, limits, and obstacles still matter. A six-joint arm may also be redundant for a task that constrains only the three-dimensional position of its tool.

## Mobile platforms: pose versus immediate motion

A **differential-drive** base uses separately driven left and right wheels. Equal forward wheel speeds move it forward; different speeds turn it. Its pose on the floor is $(x,y,\psi)$: two coordinates locate its center, and the heading angle $\psi$ tells us which way it faces.

These three numbers describe where it is. They do not mean it can slide in three independent ways. With ordinary wheels rolling without sideways slipping, its two immediate motion choices are forward/backward speed $v$ and turning rate $\omega$.

For a base pointing along global positive $x$, it can move along $x$ or turn, but it cannot immediately slide along $y$ while holding that heading. To move to its left, it can turn left, drive forward, then turn back. Its final sideways displacement results from a sequence of allowed motions.

If you know sine and cosine, this relationship is expressed by

$$
\dot{x}=v\cos\psi,\qquad \dot{y}=v\sin\psi,\qquad \dot{\psi}=\omega.
$$

A dot means a rate of change with time. At $\psi=0$, these become $\dot{x}=v$, $\dot{y}=0$, and $\dot{\psi}=\omega$. At that instant, no choice of $v$ supplies sideways velocity. Turning changes the heading and therefore the global direction of subsequent forward motion.

Here we describe chassis pose only. Wheel angles and attached mechanisms require additional coordinates if they are included in the configuration model.

## Checkpoint

Does a six-joint arm always provide six independent tool-motion directions?

No. Independence depends on its geometry, the task, and the current configuration. At a singularity, some joint motions have dependent effects on the tool, reducing instantaneous task-motion capability.

## Quick reference

| Concept | Meaning |
| --- | --- |
| Configuration | The mechanism's arrangement, described by independent coordinates |
| Pose | Position and orientation of a body or tool |
| Task dimension | Number of independent quantities the task constrains |
| Redundancy | Extra configuration freedom relative to a particular task |

[Previous](01-links-joints-and-structure.md) · [Section index](README.md) · [Next: Workspace](03-workspace-and-limitations.md)
