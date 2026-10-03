# Performance and Robot Selection

Suitability depends on the whole task: a robot must reach the required poses, carry its tooling and object, complete the cycle, and tolerate its environment.

## Payload includes tooling

Payload ratings commonly specify carried **mass** in kilograms. Weight is a force, $W=mg$, measured in newtons. Count the tool, adapters, attached sensors, and workpiece according to the manufacturer's rating convention. Load position and inertia also matter; a mass limit alone does not describe every permitted load. Manufacturer guidance explicitly considers both the gripper and the workpiece when assessing [payload and center-of-gravity limits](https://www.universal-robots.com/manuals/EN/HTML/SW10_15/Content/prod-usr-man/complianceUR8Long/H_g5_sections/mechanical_interface_g5/maximum_payload_en_g5.htm).

Suppose a hypothetical arm is rated for 5 kg under specified conditions. A 1.2 kg gripper, 0.3 kg adapter, and 2 kg workpiece total

$$
m_{\mathrm{load}}=1.2+0.3+2.0=3.5\text{ kg}.
$$

This passes the scalar mass check. If their centers of mass lie along the same flange axis at 0.05, 0.02, and 0.20 m, respectively, their combined offset is

$$
d_{\mathrm{COM}}=\frac{1.2(0.05)+0.3(0.02)+2(0.20)}{3.5}
\approx0.133\text{ m}.
$$

That offset, inertia, motion, and configuration must also fit the robot's load limits. A long tool can create substantial joint loading despite low mass.

## Compare the right quantities

| Quantity | Meaning | What it does not establish alone |
| --- | --- | --- |
| Reach | A specified maximum distance from a reference to the tool or flange | All positions or orientations inside that distance are reachable |
| Payload-to-robot-mass ratio | Rated payload mass divided by robot mass | Energy efficiency, stiffness, or installed-system mass |
| Joint speed | Angular or linear rate at a joint | Tool speed, which also depends on configuration |
| Tool speed | Translational or rotational rate of the TCP | Sustainable cycle rate including grasping and waits |
| Cycle time | Time for the complete repeatable operation | Product quality or long-term availability |

For 5 kg rated payload and 25 kg robot mass, the ratio is $5/25=0.20$. It is dimensionless. Include the same components in the denominator when comparing robots.

For a sequential cycle containing 1.2 s approach, 0.4 s gripping, 1.6 s transfer, 0.3 s release, and 1.5 s return, total time is 5.0 s. Ideal throughput is $60/5=12$ cycles/minute before delays, faults, and replenishment. Increasing maximum joint speed might not shorten a cycle dominated by waiting for a process.

## Power and operating conditions

Distinguish instantaneous power in watts from energy in joules or watt-hours. Average electrical power of 200 W over 5 s uses $E=Pt=1000$ J. For pneumatic and hydraulic systems, account for the compressor or pump as well as the robot-side hardware.

Check specified temperature, humidity, dust and liquid exposure, material compatibility, and cleanliness requirements. An ingress-protection rating addresses stated enclosure conditions; it does not automatically establish corrosion resistance, hygiene, or cleanroom suitability. Tooling and connectors may have different limits from the arm.

## Quick reference

Use [accuracy and repeatability](../01-robotics-foundations/03-from-task-to-system.md) to interpret positioning performance and [workspace](03-workspace-and-limitations.md) to evaluate reach. Protective functions such as emergency stops and collision detection belong to the complete [application assessment](../04-control-and-interaction/04-collaborative-robots.md); their presence alone is not a performance or safety guarantee.

[Previous](05-mobile-hybrid-and-soft-robots.md) · [Section index](README.md) · [Next: End effectors](07-end-effectors-and-grippers.md)
