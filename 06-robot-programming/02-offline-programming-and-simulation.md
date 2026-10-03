# Offline Programming and Simulation

**Offline programming** prepares robot behavior without needing the physical robot to execute each teaching step. It can use text editing, CAD geometry, simulation, or a virtual controller. Working from another room is not the defining feature.

## What the virtual installation needs

Model the robot, joints and limits, tool geometry and TCP, workpiece frames, fixtures, and relevant obstacles. Include load and process information when the simulation supports the required dynamics or timing analysis. A virtual controller can reproduce controller-specific program behavior more closely than geometry-only animation, but does not establish that every physical effect is modeled.

For example, [ABB RobotStudio](https://new.abb.com/products/robotics/nl/software-and-digital/robotstudio/robotstudio-desktop) supports simulation and offline programming using a virtual controller. The general workflow below applies without requiring that particular product.

## Validate in stages

| Stage | Question |
| --- | --- |
| Program logic | Are branches, tool actions, waits, and error handling defined? |
| Geometric motion | Are target poses reachable and paths clear of modeled obstacles? |
| Motion feasibility | Are joint limits, speeds, accelerations, and singularities addressed? |
| Process behavior | Are contact, tool operation, timing, and external signals represented adequately? |
| Physical integration | Do real calibration, payload, tooling, and I/O match the program's assumptions? |

Simulation checks are only as complete as the model. An unmodeled cable, misplaced fixture, or incorrect tool offset can invalidate an apparently clear path. A geometric simulator also cannot validate a grip force merely by showing the object attached to the gripper.

## Example: the fixture moved

Suppose a pickup point is stored relative to a workpiece frame. In simulation the frame origin is at $(0.4,0.2)$ m, but the physical origin is at $(0.42,0.2)$ m with the same orientation. The base-frame pickup location differs by 0.02 m along $x$.

Updating the workpiece frame can update the associated targets coherently. It does not automatically validate their new approach paths, obstacle clearances, or reachability. Retest the changed relationships before relying on the program.

## From model to execution

Export or deploy code compatible with the actual controller, then verify frame definitions, units, tool and load settings, and signal mappings. Physical commissioning uses the installation's approved modes and progressive checks; a simulation pass is one input to that process. Teaching and offline preparation often complement each other: broad motion can be prepared virtually and then calibrated or refined on the real installation.

## Quick reference

Separate what was modeled, what was checked, and what remains an assumption. A virtual controller, a collision model, and a dynamics model answer different questions. Record the version of the program and calibration used for each validation.

[Previous](01-teaching-and-playback.md) · [Section index](README.md) · [Next: Task logic](03-task-logic-and-programs.md)
