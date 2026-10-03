# Force, Impedance, and Hybrid Control

When a tool touches an object, motion and contact force become coupled. Pushing a rigid position target farther into a surface can increase load rather than produce the requested displacement.

## Force regulation

A force controller compares desired and measured contact force. Consider a one-dimensional gripper with positive velocity defined as closing. An illustrative outer-loop command is

$$
v_{\mathrm{close}}=k_F(F_d-F_a),
$$

where $F_d$ is desired force, $F_a$ measured force, and $k_F>0$ has units m/(N·s). For $F_d=5$ N, $F_a=3$ N, and $k_F=0.002$ m/(N·s), closing velocity is 0.004 m/s. If measured force exceeds the target, this convention produces opening motion.

This simple relationship assumes the mechanism makes closing increase contact force. Practical contact acquisition, saturation, filtering, and stability analysis are separate requirements. A force sensor reading zero before contact does not justify unrestricted closing speed.

## Impedance: choose how motion responds to contact

An impedance objective specifies a relationship between external force and displacement, velocity, and acceleration. A scalar desired behavior is

$$
M_d\ddot{e}+D_d\dot{e}+K_d e=F_{\mathrm{ext}},\qquad e=x-x_d,
$$

with positive external force along positive $x$ and a fixed equilibrium $x_d$. The virtual mass $M_d$, damping $D_d$, and stiffness $K_d$ describe the intended response. Here the displacement-error sign differs from the desired-minus-measured convention used for tracking; it is stated explicitly so the spring relationship is clear.

At static equilibrium, velocity and acceleration are zero, leaving $K_d e=F_{\mathrm{ext}}$. With $K_d=200$ N/m and $F_{\mathrm{ext}}=4$ N, displacement is $e=4/200=0.02$ m. A larger stiffness gives less displacement under the same load.

This equation describes desired behavior, not a complete motor-torque formula. An **admittance controller** commonly takes measured force as input and generates a motion reference that realizes a chosen dynamic relationship. Interface choice, sensing, and the underlying servo determine implementation.

## Hybrid motion–force control

For a tool wiping a surface, define a local normal direction perpendicular to the surface and tangential directions along it. Regulate normal force while commanding tangential motion. Do not independently demand incompatible rigid position and force values along the same constrained direction. This direction-based division is the central idea of [hybrid motion–force control](https://modernrobotics.northwestern.edu/nu-gm-book-resource/11-6-hybrid-motion-force-control/).

For a horizontal surface with normal along $z$, a task might request 4 N normal contact, 0.02 m/s tangential speed along $x$, and a suitable tool orientation. An unknown or curved surface requires updating the estimated normal; global $z$ will not always be the contact-normal direction.

“Hybrid” here means different control objectives in different directions. [Hybrid visual servoing](../05-perception-and-autonomous-grasping/02-visual-servoing.md) combines different visual error descriptions instead.

## Quick reference

| Approach | Main objective |
| --- | --- |
| Force control | Regulate measured force toward a reference |
| Impedance control | Shape the relationship between motion and interaction force |
| Hybrid motion–force control | Assign motion and force objectives to appropriate task directions |

[Previous](02-position-paths-and-trajectories.md) · [Section index](README.md) · [Next: Collaborative robots](04-collaborative-robots.md)
