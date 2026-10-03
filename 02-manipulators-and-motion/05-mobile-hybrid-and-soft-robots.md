# Mobile, Hybrid, and Soft Robots

Robot descriptions can refer to locomotion, mechanical structure, or behavior. These categories overlap: one machine can be a wheeled mobile manipulator with an adaptive controller and a soft gripper.

## Moving the base

| Platform | How it moves | Useful capabilities | Constraints to examine |
| --- | --- | --- | --- |
| Wheeled | Wheels roll; some designs also steer | Efficient travel on suitable firm surfaces; warehouse transport and road vehicles | Wheel slip, turning geometry, steps, and ground clearance |
| Tracked | Driven tracks distribute contact over a larger area | Traction and reduced ground pressure on suitable rough or soft terrain; inspection, agriculture, and rescue | Skid-steering losses, surface disturbance, and terrain-dependent slip |
| Legged | Jointed legs place feet at selected contacts | Stepping over obstacles and selecting footholds; research and inspection | Balance, contact planning, impact loads, and energy demand |

Legs do not automatically guarantee stability on uneven ground. The robot must find suitable contacts and control its body relative to them. Suspension can accommodate terrain, but its coordinates may be passive rather than independently commanded.

## Count the quantities your model includes

A differential-drive robot commonly has two driven wheels and planar chassis pose $(x,y,\psi)$. The two motor inputs are not a count of three-dimensional chassis pose coordinates. The [DOF lesson](02-degrees-of-freedom.md) explains why rolling also restricts immediate sideways motion.

Similarly, a two-track skid-steer base typically has separately driven left and right tracks; it does not have one total DOF simply because its propulsion uses tracks. Steering depends on their relative speeds and contact slip.

For a legged robot, count the joints actually present. A quadruped with three actuated joints per leg has $4\times3=12$ actuated joint coordinates. An unconstrained floating-base model adds six body-pose freedoms before foot-contact constraints are imposed. Neither “three per leg” nor a particular total applies to every legged design.

## Humanoid, hybrid, adaptive, and soft

| Description | What it tells you | What it does not determine |
| --- | --- | --- |
| Humanoid | Body arrangement resembles some aspects of human anatomy | A fixed joint count, balance capability, or level of intelligence |
| Hybrid mechanism | Combines structures, such as a serial arm on a parallel positioning stage | One standard joint sequence or DOF count |
| Adaptive robot | Changes controller parameters or behavior from online information | A particular mechanical structure |
| Soft robot | Uses substantial compliant or deformable structures | Necessarily few DOF or intrinsically safe contact |

A soft finger can bend continuously along its length. A detailed deformation model may require many variables; a simplified model might approximate the finger using one curvature variable. One pressure input can influence many deformation modes, so **actuator count and shape-model dimension are different**.

Compliance can help a gripper conform to produce or another delicate object, but applied pressure, contact area, tool edges, and stored energy still matter. An exoskeleton can use rigid, soft, or combined construction; its application does not uniquely identify its mechanism.

## Checkpoint

A wheeled robot has an arm, a soft gripper, and software that changes grip force when slip is detected. Which label describes which part?

“Wheeled” describes locomotion, “manipulator” describes the arm, “soft” describes the gripper construction, and “adaptive” describes the force-control behavior. No single label replaces a description of the complete system.

## Quick reference

Count configuration variables, contact constraints, and control inputs separately. Choose terrain capability from the actual mechanism and contact conditions. Treat adaptability as behavior and softness as a modeling and construction choice.

[Previous](04-robot-configurations.md) · [Section index](README.md) · [Practice](exercises.md)
