# End Effectors and Grippers

An end effector is the robot's task-facing tool. A gripper holds an object; a welding torch, polishing head, dispenser, cutter, or inspection probe can perform work without gripping it.

## Separate function, actuation, and construction

| Classification | Examples | Question answered |
| --- | --- | --- |
| Holding principle | Mechanical fingers, vacuum, magnetic attraction, adhesion | How is the object retained? |
| Actuation | Electric motor, pneumatic cylinder, hydraulic cylinder | Where does the driving effort come from? |
| Construction | Rigid, compliant, soft, bioinspired | How does the tool move or conform? |
| Sensing and control | Force sensing, slip detection, adaptive grip | How is task progress measured and adjusted? |

A soft pneumatic finger gripper belongs to several categories simultaneously. “Pneumatic” is not a competing holding principle to “mechanical”: air pressure can drive mechanical jaws. Hydraulic actuation can supply substantial force, but power infrastructure, leakage, and control requirements affect suitability.

## Match the holding principle to the object

| Principle | Useful situations | Limitations to investigate |
| --- | --- | --- |
| Mechanical fingers | Parts with accessible contact surfaces | Opening, finger clearance, friction, contact pressure, and release |
| Vacuum | Objects with a surface that supports an adequate seal | Leakage, porosity, curvature, peel loading, and vacuum loss |
| Magnetic | Magnetically responsive workpieces | Material response, thickness, air gaps, residual magnetism, and release |
| Adhesive or dry adhesion | Compatible surfaces with suitable contact area | Contamination, repeat use, peeling, and residue where applicable |

Not all metals are strongly attracted by a practical magnetic gripper. Aluminum, for example, is not handled like ferromagnetic steel. A vacuum cup uses a pressure difference across its effective area; it does not require a perfect vacuum.

## Worked vacuum estimate

For an ideal sealed cup with pressure difference $\Delta p$ and effective area $A$, normal holding force is approximately

$$
F=\Delta p A.
$$

With $\Delta p=40{,}000$ Pa and $A=5\times10^{-4}$ m², $F=20$ N. A 1 kg object weighs approximately 9.81 N. The ideal force exceeds the static weight, but this does not establish a usable lift: leaks, acceleration, cup deformation, load direction, and moments reduce the useful margin. Use validated component ratings and the actual load case.

## Tools that combine operations

A hybrid tool may grip and inspect in one assembly. A wrist force/torque sensor measures interaction loads; a mounted camera can guide alignment. Extra devices change tool mass, clearance, wiring, and the [TCP offset](01-links-joints-and-structure.md).

Bioinspired tools borrow features such as compliant fingers, suction structures, or surface adhesion. Their inspiration does not determine effectiveness on every object. An entire swimming robot is a locomotion platform; it becomes relevant to end-effector design only when its task tool is being considered.

## Quick reference

Start with object material, geometry, mass, tolerated contact load, and access. Then choose the holding principle, actuator, sensors, and release method. See [adaptive grasping](../05-perception-and-autonomous-grasping/04-adaptive-grasping.md) for force and slip feedback rather than assuming conformity alone ensures a successful grip.

[Previous](06-performance-and-selection.md) · [Section index](README.md) · [Practice](exercises.md)
