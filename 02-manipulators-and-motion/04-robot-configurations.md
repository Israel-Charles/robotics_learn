# Robot Configurations

Which arrangement makes a task easy to reach and execute? Compare joint geometry, usable workspace, and tool-orientation requirements before comparing speed or payload.

## Read a joint sequence

For a serial mechanism, read the joint letters from base to tool: `R` means revolute and `P` means prismatic. `RPP` therefore describes one rotation followed by two translations. The letters alone do not specify axis directions: two mechanisms with the same sequence can move very differently.

The counts below describe the stated ideal mechanism, with independent joints. Extra wrist joints or tool mechanisms add coordinates.

| Arrangement | Typical structure | DOF of stated mechanism | Motion and workspace intuition | Typical uses and tradeoffs |
| --- | --- | --- | --- | --- |
| Cartesian | `PPP`, three perpendicular linear axes | 3 | Independent translation along three axes; box-shaped workspace for rectangular travel limits | Gantries, pick-and-place, and the positioning stages of many printers and CNC machines; simple geometry but substantial supporting structure |
| Cylindrical | `RPP`: base rotation, vertical slide, radial slide | 3 | Sweeps a radial and vertical range around a base; cylindrical region or sector | Material handling and machine loading; convenient access around a base but limited tool orientation without a wrist |
| Spherical or polar | `RRP`: azimuth, elevation, radial extension | 3 | Points an extending arm in different directions; spherical-shell region or sector | Reaching into a surrounding volume; tool access depends on angular limits and extension |
| Articulated | `RRR` positioning chain; often additional wrist joints | 3 for that chain; commonly 6 for a complete industrial arm | Bends around obstacles within a curved workspace | Assembly, welding, painting; flexible access but coupled motion and singularities |
| SCARA | Two parallel rotary axes and vertical travel; commonly `RRPR` with tool rotation | 3 for `RRP` positioning; 4 with tool rotation | Horizontal two-link reach plus vertical travel | Fast transfer and assembly; conventional design does not provide arbitrary tool tilt |
| Delta | Multiple arms connect one fixed base to one moving platform | Classic positioning platform has 3 translational DOF; variants add orientation axes | Several chains move together while constraining platform orientation | Rapid sorting and packaging; payload, clearance, and workspace depend on design |

These are engineering tendencies, not performance guarantees. Repeatability and speed also depend on construction, calibration, load, and control.

## Why polar and SCARA can both contain RRP

A polar arm turns around a vertical base axis, tilts about a different axis, and extends radially. A SCARA's first two rotary axes are parallel, allowing its two links to sweep horizontally; its prismatic joint provides vertical travel. Their identical three-letter positioning sequence does not capture those axis relationships.

SCARA is commonly expanded as **Selective Compliance Assembly Robot Arm**; “Selective Compliance Articulated Robot Arm” is also used. Selective compliance refers to different mechanical response in different directions, traditionally allowing some horizontal accommodation while remaining relatively stiff vertically for assembly.

## A delta is a parallel mechanism

```text
                 fixed base
             /       |       \
          chain 1  chain 2  chain 3
             \       |       /
                moving platform
                     tool
```

This is a connectivity sketch, not a drawing of the joint axes. The classic delta uses driven base joints and additional passive joints and parallelogram linkages. Its platform translates while the linkages constrain its orientation. Calling it simply `RRR` would incorrectly suggest one serial chain of three joints. A three-input mechanism need not produce three rotational outputs; the linkage converts coordinated inputs into platform translation. See the primary research example [DeltaZ](https://arxiv.org/abs/2207.00721) for a three-translation delta design.

Parallel mechanisms are a broader family. A Stewart-type platform, for example, can use six actuated extensible legs with passive joints to control a platform's spatial pose. Parallel construction can offer stiffness and low moving mass, but closed-loop constraints can reduce workspace and complicate the motion model.

## Worked selection example

A task transfers upright parts between points on a flat table, lifts them vertically, and turns them about the vertical axis. That requires control of $x,y,z$, and yaw. A conventional four-axis SCARA fits this motion description. If the task must also tilt a part to reach an angled opening, check additional orientation capability; merely reaching the opening's position is insufficient. An articulated arm with a suitable wrist is another candidate.

## Quick reference

- Joint sequence describes joint types; axis arrangement determines their geometric effect.
- State whether a DOF count includes the wrist and end effector.
- Delta and other parallel robots require a description of their multiple chains.
- Match reachable poses, payload, and paths to the task before comparing advertised speed.

[Previous](03-workspace-and-limitations.md) · [Section index](README.md) · [Next: Mobile, hybrid, and soft robots](05-mobile-hybrid-and-soft-robots.md)
