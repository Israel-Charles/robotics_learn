# What Is Robotics?

Robotics studies the design, construction, operation, and application of machines that act in the physical world. A robot must connect a computational decision to a physical action: moving a wheel, positioning a tool, opening a gripper, or changing a flight trajectory.

That connection makes robotics interdisciplinary. A correct program cannot compensate for every mechanical weakness, and a well-built mechanism still needs appropriate power, sensing, and control.

## The disciplines working together

| Discipline | Questions it helps answer | Example in a pick-and-place system |
| --- | --- | --- |
| Mechanical engineering | What can move? What loads can the structure support? | Choose arm geometry and size the gripper |
| Electrical engineering | How are components powered, driven, and connected? | Supply motors and interface encoders |
| Computer science | How are instructions represented, coordinated, and executed? | Sequence grasping and placement operations |
| Control engineering | How does actual motion track desired motion? | Adjust motor effort from measured position error |
| Artificial intelligence | How can the system infer or choose behavior from complex information? | Recognize an unfamiliar object in a camera image |

AI is one possible tool within robotics. A robot following a taught welding path can operate effectively without a learned model or an AI planner.

## Kinematics, dynamics, and control

These subjects answer different questions about the same mechanism:

- **Kinematics:** How do joint positions relate to tool position and orientation? How do their velocities relate?
- **Dynamics:** What forces and torques produce motion, given mass, inertia, gravity, and other loads?
- **Control:** How should actuator commands change so that measured behavior follows the desired behavior?

Suppose an arm must move its gripper upward by 0.1 m. Kinematics helps determine the joint motion. Dynamics helps estimate the torque required to accelerate the arm and its payload. Control uses measurements to reduce tracking error during execution.

A geometrically reachable point is therefore not necessarily a point the robot can reach under every load or at every speed.

## Applications and the demands they create

| Application | Typical action | Important engineering concern |
| --- | --- | --- |
| Manufacturing | Weld, assemble, paint, or transfer parts | Repeatable tool motion and cycle time |
| Agriculture | Inspect crops or handle produce | Variable terrain and delicate objects |
| Medical robotics | Position an instrument or assist a procedure | Precise motion and interaction with people |
| Inspection | Observe equipment or infrastructure | Access, sensing coverage, and reliability |
| Exploration | Traverse unfamiliar environments | Limited communication and uncertain terrain |
| Logistics | Move goods between locations | Navigation and coordination with surrounding activity |

The same mathematical ideas appear across applications, but the physical constraints differ. A gripper suitable for a rigid metal part may damage soft fruit even if both objects have the same size.

## Checkpoint

An arm reaches the right location with no payload but sags when carrying a heavy object. Is this purely a kinematics problem?

No. Geometry still matters, but structural deflection, loading, actuator capability, and control can affect the outcome. An ideal rigid-body kinematic model does not explain all of those effects.

## Quick reference

| Term | Main focus |
| --- | --- |
| Kinematics | Motion geometry and motion relationships |
| Dynamics | Forces, torques, mass, and motion |
| Control | Making actual behavior follow desired behavior |
| Robotics | Integrating these ideas into physical systems |

[Section index](README.md) · [Next: Robots, manipulators, and autonomy](02-robots-manipulators-and-autonomy.md)
