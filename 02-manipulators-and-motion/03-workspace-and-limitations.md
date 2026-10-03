# Workspace and Motion Limitations

A robot's **workspace** describes the positions or poses its tool can achieve under stated assumptions. Always specify whether orientation, joint limits, obstacles, and tool offsets are included.

## Reachable positions for a planar arm

Consider an ideal planar arm with two revolute joints, link lengths $L_1$ and $L_2$, unrestricted joint rotation, and a tool at the second link's tip. Ignore collisions and link thickness.

The distance $r$ from the base to the tool satisfies

$$
|L_1-L_2| \leq r \leq L_1+L_2.
$$

The greatest distance occurs when the links point in the same direction. The smallest occurs when they fold back against each other. With unrestricted base rotation, the reachable position workspace is an annulus, or a disk if the lengths are equal.

For $L_1=0.4$ m and $L_2=0.3$ m:

$$
0.1\text{ m} \leq r \leq 0.7\text{ m}.
$$

A target at $(0.3,0.4)$ m has $r=\sqrt{0.3^2+0.4^2}=0.5$ m and passes this ideal geometric test. A target only 0.05 m from the base does not, even though it looks “close.”

## Position reach is not arbitrary orientation reach

At a reachable position, the arm may have only a limited set of possible tool orientations. The **dexterous workspace** is commonly used to describe positions at which all orientations required by a specified definition or task can be achieved. State the orientation requirement whenever using the term.

For the two-joint planar arm, selecting $(x,y)$ usually leaves only discrete elbow choices, not an independently adjustable orientation. A third joint can add orientation freedom, subject to geometry and limits.

## Singularities

A **kinematic singularity** is a configuration where the tool loses an independent direction of instantaneous motion that is available at ordinary configurations. “Instantaneous” means the velocity at the current configuration, before the geometry has changed.

Consider a two-link arm stretched horizontally to the right:

```text
base o-----------o-----------o TCP
               elbow          ↑↓ available tip velocity
                         ←→ no independent tip velocity here
```

Turning only the shoulder starts the tip moving tangent to a circle centered at the base. Turning only the elbow starts it moving tangent to a circle centered at the elbow. At this straight configuration, both tangents are vertical. Combining those joint motions can change the vertical velocity, but cannot produce a horizontal velocity at that instant.

The joints still move; their immediate effects on tool position point along the same line. This is what “losing an independent direction” means. In matrix terminology, the joint-to-tool velocity mapping **loses rank**: its outputs no longer span as many independent directions. You do not need matrix calculations to recognize the two parallel tangents in this example.

### Why can bending still bring the tip inward?

Hold the shoulder fixed at zero and bend the elbow through a small angle $\delta$. The second link tip moves along a circle:

$$
\Delta x=L_2(\cos\delta-1),\qquad \Delta y=L_2\sin\delta.
$$

For $L_2=0.3$ m and $\delta=1^\circ$, the changes are approximately $-0.0000457$ m horizontally and $+0.00524$ m vertically. There is an inward displacement after a finite turn. However, at the exact starting instant the tangent is vertical: the horizontal displacement per unit angle tends to zero as the turn tends to zero. This distinguishes a finite change in position from the starting velocity.

Straight and fully folded configurations are singular for this arm's position task. Near a singularity, generating certain requested tool velocities may require very large joint velocities. A singularity does not mean that every motion is impossible or that a joint has mechanically locked.

## Real limitations beyond the geometric model

| Constraint | Why it matters |
| --- | --- |
| Joint travel limits | Remove some otherwise geometric solutions |
| Self-collision and obstacles | Can prevent a pose or the path to it |
| Tool geometry | Changes reach and clearance |
| Payload and torque limits | Restrict what can be held or moved |
| Speed and acceleration limits | Restrict how quickly motion can occur |
| Calibration and compliance | Cause actual motion to differ from ideal geometry |

Check both the final configuration and the path taken to reach it. Two feasible endpoints do not guarantee that a straight interpolation between them is collision-free.

## Quick reference

- Ideal planar 2R radial reach: $|L_1-L_2|\leq r\leq L_1+L_2$.
- A position solution does not automatically satisfy an orientation requirement.
- Singularity concerns instantaneous task-motion capability.
- Geometric reachability is one part of feasibility.

[Previous](02-degrees-of-freedom.md) · [Section index](README.md) · [Practice](exercises.md)
