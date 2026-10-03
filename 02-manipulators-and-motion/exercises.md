# Exercises · Manipulators and Motion

1. **Joint coordinates.** An ideal fixed-base serial chain contains an R joint, a P joint, and an R joint, with no coupling or closed loop. Write its configuration variables, their units, and its DOF.
2. **Tool pose.** A planar 2R arm has joint angles $30^\circ$ and $-20^\circ$. With an aligned tool, what is its orientation relative to the base? Can you generally specify a different orientation while keeping an arbitrary fixed tool position?
3. **Reach.** For unrestricted planar links of 0.5 m and 0.2 m, find the minimum and maximum tool distances from the base. Are positions at radii 0.1 m, 0.4 m, and 0.8 m reachable in the ideal model?
4. **Joint count.** Consider the movable planar four-bar linkage in [Links, joints, and robot structure](01-links-joints-and-structure.md), with one bar fixed and four pin joints. At an ordinary configuration on one assembly branch, can you choose all four joint angles independently? Explain what would happen if you chose incompatible angles and why four pin joints do not imply four mechanism DOF.
5. **Mobile motion.** A differential-drive robot uses ordinary left and right wheels that roll without sideways slipping. Its chassis pose is $(x,y,\psi)$. If it faces positive $x$, can it immediately slide along $y$ without changing its heading? Name its two immediate motion choices and describe a sequence that moves it to its left.
6. **Singularity.** Sketch a fully extended 2R arm pointing along positive $x$. Imagine first rotating only the shoulder and then only the elbow. For each case, identify the circle traced by the tip and its tangent at the starting point. Which tip-velocity direction is missing at that instant? Explain why the tip can nevertheless move inward after a finite elbow bend.

7. **Configuration comparison.** Explain why polar and SCARA positioning mechanisms can both be described as RRP yet have different motion. Why is RRR alone an inadequate description of a delta robot? Which conventional SCARA task freedoms include tool yaw?
8. **Count the model.** A quadruped has three actuated joints per leg. Count its actuated joint coordinates and the coordinates of an unconstrained floating-base model before contact constraints. Does a soft gripper with one pressure input necessarily have one deformation DOF? Explain.

9. **Joint freedom and actuation.** Compare the DOF of cylindrical, helical, universal, and spherical joints. For a screw with 2 mm lead, find axial travel for half a turn. Does adding an encoder make a passive hinge active? Can a passive joint dissipate energy?
10. **Load and cycle.** A hypothetical 5 kg payload-rated arm has mass 25 kg. It carries a 1.2 kg tool, a 0.3 kg adapter, and a 2 kg object. Find total load mass, nominal payload-to-robot-mass ratio, and ideal cycles per minute for a 5 s cycle. Does the mass check alone establish suitability?
11. **Gripper classification.** Explain how one gripper can be both mechanical and pneumatic. Estimate ideal normal holding force for a sealed vacuum cup with pressure difference 40,000 Pa and effective area $5\times10^{-4}$ m². Does this alone validate lifting a 1 kg object?

[Solutions](solutions.md) · [Section index](README.md)
