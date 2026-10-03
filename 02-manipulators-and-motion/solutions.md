# Worked Solutions · Manipulators and Motion

Each exercise is repeated below so you can read its reasoning alongside the question. Attempt the [exercises](exercises.md) first.

## 1. Joint coordinates

**Question.** An ideal fixed-base serial chain contains an R joint, a P joint, and an R joint, with no coupling or closed loop. Write its configuration variables, their units, and its DOF.

**Solution.**

An R joint contributes one angular coordinate; a P joint contributes one displacement coordinate. A configuration vector is

$$
q=\begin{bmatrix}\theta_1\\d_2\\\theta_3\end{bmatrix}.
$$

| Joint | Variable | Unit |
| --- | --- | --- |
| First revolute joint | $\theta_1$ | rad |
| Prismatic joint | $d_2$ | m |
| Last revolute joint | $\theta_3$ | rad |

The vector can contain different physical units because each entry describes a different joint. With no coupling or loop constraints, each variable can be adjusted independently, so the count is $1+1+1=3$ DOF. This counts configuration freedoms; it does not prove the tool can independently move in every possible task direction.

## 2. Tool pose

**Question.** A planar 2R arm has joint angles $30^\circ$ and $-20^\circ$. With an aligned tool, what is its orientation relative to the base? Can you generally specify a different orientation while keeping an arbitrary fixed tool position?

**Solution.**

The first link points $30^\circ$ from the base's positive $x$ axis. The elbow turns the second link $20^\circ$ clockwise relative to the first:

$$
\phi=\theta_1+\theta_2=30^\circ+(-20^\circ)=10^\circ.
$$

The aligned tool therefore points $10^\circ$ counterclockwise from base $x$.

To keep a fixed target position, both $x$ and $y$ must remain correct. Changing a joint angle to change orientation generally also moves the tip. The other joint cannot generally compensate in both position coordinates while providing an arbitrarily chosen orientation. There are two adjustable angles but three requested pose quantities.

For a concrete example, the farthest-right tip position forces both links to point right, so an aligned tool cannot point upward there. At many interior positions, two different elbow configurations are possible, giving two orientations to choose from. Two alternatives still do not allow every orientation. Special configurations, such as equal links folded exactly onto the base, need separate treatment.

## 3. Reach

**Question.** For unrestricted planar links of 0.5 m and 0.2 m, find the minimum and maximum tool distances from the base. Are positions at radii 0.1 m, 0.4 m, and 0.8 m reachable in the ideal model?

**Solution.**

Maximum reach occurs when the links point in the same direction:

$$
r_{\max}=L_1+L_2=0.5+0.2=0.7\text{ m}.
$$

Minimum reach occurs when the shorter link folds back along the longer:

$$
r_{\min}=|L_1-L_2|=|0.5-0.2|=0.3\text{ m}.
$$

Thus the ideal radius must satisfy $0.3\leq r\leq0.7$ m.

| Target radius | Check | Reachable in the stated ideal model? |
| --- | --- | --- |
| 0.1 m | $0.1<0.3$ | No; the links cannot fold close enough to the base |
| 0.4 m | $0.3\leq0.4\leq0.7$ | Yes |
| 0.8 m | $0.8>0.7$ | No; it exceeds full extension |

Unrestricted base rotation lets the annular region extend around the base. Limits and obstacles would require additional checks.

## 4. Joint count

**Question.** Consider the movable planar four-bar linkage in [Links, joints, and robot structure](01-links-joints-and-structure.md), with one bar fixed and four pin joints. At an ordinary configuration on one assembly branch, can you choose all four joint angles independently? Explain what would happen if you chose incompatible angles and why four pin joints do not imply four mechanism DOF.

**Solution.**

The four pin joints each permit relative rotation, but the rigid bars must also remain connected into a loop. These are simultaneous requirements.

Imagine setting the left bar's angle. Its upper endpoint is now fixed. The remaining upper and right bars must connect that point back to the fixed right-hand ground pivot while retaining their lengths. At an ordinary movable configuration, on a chosen assembly branch, their angles follow from that requirement. You cannot independently turn each pin to an arbitrary angle without either stretching a rigid bar or separating a joint.

Consequently, this ordinary four-bar mechanism generally has one independent motion, even though it contains four rotating joints. Counting joint freedoms as $1+1+1+1=4$ neglects the loop-closure constraints. The lesson's rule “one independent coordinate per one-DOF joint” applies to an uncoupled open serial chain, not automatically to a closed loop.

## 5. Mobile motion

**Question.** A differential-drive robot uses ordinary left and right wheels that roll without sideways slipping. Its chassis pose is $(x,y,\psi)$. If it faces positive $x$, can it immediately slide along $y$ without changing its heading? Name its two immediate motion choices and describe a sequence that moves it to its left.

**Solution.**

The three pose numbers have different roles: $x,y$ locate the chassis center, and $\psi$ describes its heading. They describe a state, not three independent movement commands.

With the heading at $\psi=0$, the no-side-slip model gives

$$
\dot{x}=v\cos0=v,\qquad \dot{y}=v\sin0=0,\qquad \dot{\psi}=\omega.
$$

The two immediate choices are forward/backward speed $v$ and turning rate $\omega$. No choice of $v$ gives a sideways velocity while the heading stays at zero.

To move to its left, the robot can turn $90^\circ$ counterclockwise, drive forward a chosen distance, and turn $90^\circ$ clockwise to restore its original heading. During the drive it faces global positive $y$, so $\dot{x}=0$ and $\dot{y}=v$. It ends up displaced sideways relative to its original heading using a sequence of rolling motions, without ever sliding sideways through its wheels.

## 6. Singularity

**Question.** Sketch a fully extended 2R arm pointing along positive $x$. Imagine first rotating only the shoulder and then only the elbow. For each case, identify the circle traced by the tip and its tangent at the starting point. Which tip-velocity direction is missing at that instant? Explain why the tip can nevertheless move inward after a finite elbow bend.

**Solution.**

At full extension along positive $x$:

```text
base o---------------o----------o tip
                   elbow         ↑ tangent for either joint
```

With the elbow fixed, shoulder rotation carries the tip on a circle of radius $L_1+L_2$ about the base. With the shoulder fixed, elbow rotation carries the tip on a circle of radius $L_2$ about the elbow. At the rightmost point of either circle, the tangent is vertical. Either sign of rotation gives upward or downward velocity; combinations remain vertical. Independent horizontal tip velocity is missing at this instant.

After a finite elbow bend $\delta$, with the shoulder held at zero, compare the new and old tip coordinates:

$$
\begin{aligned}
x_{\mathrm{old}}&=L_1+L_2,& y_{\mathrm{old}}&=0,\\
x_{\mathrm{new}}&=L_1+L_2\cos\delta,& y_{\mathrm{new}}&=L_2\sin\delta.
\end{aligned}
$$

Subtracting gives $\Delta x=L_2(\cos\delta-1)$ and $\Delta y=L_2\sin\delta$. For a small nonzero bend, $\cos\delta<1$, so $\Delta x<0$: the tip has moved inward. There is no contradiction. Its starting tangent is vertical, but the tangent changes as the elbow bends. Finite displacement includes that change in geometry.

## 7. Configuration comparison

**Question.** Explain why polar and SCARA positioning mechanisms can both be described as RRP yet have different motion. Why is RRR alone an inadequate description of a delta robot? Which conventional SCARA task freedoms include tool yaw?

**Solution.** The joint letters do not specify axis arrangement. A polar mechanism changes azimuth, elevation, and radial extension; a SCARA uses two parallel rotary axes for horizontal reach and a vertical slide. A delta contains several chains, passive joints, and closed-loop constraints; RRR could be mistaken for a single serial chain and does not describe that topology. A conventional four-axis SCARA controls horizontal position, vertical position, and tool yaw: $x,y,z,\psi$. Arbitrary roll and pitch are not additional independent freedoms of that configuration.

## 8. Count the model

**Question.** A quadruped has three actuated joints per leg. Count its actuated joint coordinates and the coordinates of an unconstrained floating-base model before contact constraints. Does a soft gripper with one pressure input necessarily have one deformation DOF? Explain.

**Solution.** Four legs times three actuated joints gives $4\times3=12$ actuated joint coordinates. A freely moving base adds six pose freedoms, so this model has $12+6=18$ configuration DOF before imposing contacts. The base freedoms are not six extra actuators. Foot contacts constrain allowable motion, depending on contact assumptions.

A soft gripper's one pressure command can influence a continuous deformation field. A reduced model might approximate that shape with one or a few variables, but actuator count does not establish the number of independent deformation modes in the physical structure.

[Exercises](exercises.md) · [Section index](README.md) · [Next section](../03-kinematics-foundations/README.md)
