# Teaching and Playback

Robot programming specifies motion, tool actions, conditions, and responses to events. It includes more than recording positions.

## Online means using the actual robot

In this context, **online programming** involves teaching or editing with the physical robot and its controller. It does not mean internet-connected programming or that normal production continues during teaching. The required operating mode and access arrangements depend on the installation.

| Method | What the operator does | What must be recorded or specified |
| --- | --- | --- |
| Teach pendant | Jogs the robot using a handheld interface and records targets | Frames, tool configuration, motion type, speed, and tool/I/O actions |
| Lead-through or hand guidance | Physically guides a robot designed and configured for that teaching mode | Selected waypoints or a sampled motion, depending on system capability |
| Playback | Executes previously recorded or programmed behavior | Interpolation, timing, event conditions, and responses to faults |

Playback can follow pendant teaching, hand guidance, or offline programming. Hand guidance does not necessarily record a continuous path automatically; some systems record only explicitly selected points.

## A point does not define the route to it

Two taught endpoint poses can be joined by different motions. Interpolating joint angles does not generally produce a straight TCP path. A Cartesian linear instruction attempts a straight tool-position path while also satisfying its orientation convention and the robot's constraints.

A recorded target also needs a frame. If a fixture moves, the same numerical coordinates in the base frame may no longer describe the required pickup pose. Use a calibrated workpiece frame where appropriate, and verify all transformed targets and paths after a setup change.

## Worked teaching sequence

For a fixed-fixture transfer, define a pickup approach pose, pickup pose, retract pose, placement approach, and placement pose. Add the actions and conditions:

1. Confirm the part and destination are ready.
2. Approach, enter the pickup pose, and close the gripper.
3. Verify the grasp before retracting and transferring.
4. Place and release, confirm release, then withdraw.

Repeating these targets assumes that fixture geometry, TCP, payload, and operating conditions remain appropriate. Successful teaching once does not prove that every later object is present or correctly seated.

## Playback versus learning

Playback reproduces stored behavior under defined parameters. [Learning from demonstrations](../05-perception-and-autonomous-grasping/05-learning-from-demonstrations.md) builds a representation from examples, potentially allowing adaptation to new task frames. A recorded path alone is not evidence that a robot has learned how to generalize the task.

## Quick reference

Online refers to using the physical system. Teaching supplies targets or motion samples; execution also requires frames, timing, interpolation, and event logic. Hand guidance is a supported operating capability, not permission to push any powered robot by hand.

[Section index](README.md) · [Next: Offline programming](02-offline-programming-and-simulation.md)
