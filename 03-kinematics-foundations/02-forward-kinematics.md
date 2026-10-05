# Forward Kinematics of a Planar Arm

**Forward kinematics** computes tool position and orientation from joint configuration. Once geometry, joint values, and conventions are specified, the ideal rigid serial model gives one tool pose.

## Define the mechanism first

Our arm has two revolute joints and link lengths $a_1,a_2>0$:

- The first joint is at the base-frame origin.
- At zero joint angles, both links extend along positive $x$.
- $\theta_1$ is the counterclockwise rotation of link 1 from base $x$.
- $\theta_2$ is the counterclockwise rotation of link 2 relative to link 1.
- The TCP is at the tip of link 2, and tool orientation follows link 2.

The symbols $a_1,a_2$ denote fixed geometric lengths, not joint angles. They also match the common-normal distances in this arm's [standard DH model](../07-spatial-kinematics/08-denavit-hartenberg.md). In the Python example, their descriptive names are `linkLength1` and `linkLength2`.

```text
                       TCP (x, y)
                      /
                 a2  /  absolute angle: θ1 + θ2
                    o  elbow
                   /
              a1  /  absolute angle: θ1
                 o--------------------> base x
               base
```

The sketch shows the connection order; actual angles vary with configuration.

## Add the link displacements

The elbow position is

$$
x_e=a_1\cos\theta_1,\qquad y_e=a_1\sin\theta_1.
$$

Link 2 is oriented at $\theta_1+\theta_2$ relative to the base. Adding its displacement gives

$$
\boxed{x=a_1\cos\theta_1+a_2\cos(\theta_1+\theta_2)}
$$

$$
\boxed{y=a_1\sin\theta_1+a_2\sin(\theta_1+\theta_2)}
$$

$$
\boxed{\phi=\theta_1+\theta_2.}
$$

### Why is tool orientation the same as link 2's angle?

We chose a tool whose direction is aligned with link 2. The same direction therefore has two descriptions: “link 2's absolute angle” describes the link, and “tool orientation” describes the attached tool. Both equal $\theta_1+\theta_2$ **for this mounting convention**.

For example, at $\theta_1=30^\circ$ and $\theta_2=60^\circ$, link 2 points at $90^\circ$. An aligned tool also points at $90^\circ$. If the tool is mounted at a fixed $20^\circ$ angle to link 2, its direction is instead

$$
\phi=\theta_1+\theta_2+20^\circ=110^\circ.
$$

This example changes orientation only and retains the TCP at the link tip. A physical attachment that also shifts the TCP requires an additional position offset, as explained in [Links, joints, and robot structure](../02-manipulators-and-motion/01-links-joints-and-structure.md).

Using $\theta_2$ alone for link 2's base-frame direction would mix a relative angle with an absolute angle.

The same geometry can be written using planar homogeneous transforms:

$$
T=\operatorname{Rot}(\theta_1)\operatorname{Trans}_x(a_1)
\operatorname{Rot}(\theta_2)\operatorname{Trans}_x(a_2),
$$

where $\operatorname{Rot}$ is the homogeneous rotation from the preceding lesson and $\operatorname{Trans}_x(a)$ has identity rotation and translation $[a,0]^T$. The final transform's translation column contains $(x,y)$ and its rotation corresponds to $\phi$.

## Worked example

Let $a_1=0.4$ m, $a_2=0.3$ m, $\theta_1=30^\circ$, and $\theta_2=60^\circ$. The second link's absolute angle is $90^\circ$.

$$
x=0.4\cos30^\circ+0.3\cos90^\circ\approx0.3464\text{ m}
$$

$$
y=0.4\sin30^\circ+0.3\sin90^\circ=0.5000\text{ m}
$$

The tool orientation is $90^\circ$. Its distance from the base is approximately 0.6083 m, within the ideal radial range of 0.1–0.7 m.

## Optional Python calculation

```python
import math

linkLength1 = 0.4
linkLength2 = 0.3
jointAngle1 = math.radians(30)
jointAngle2 = math.radians(60)

# Link 2's direction includes the rotation inherited from link 1.
toolAngle = jointAngle1 + jointAngle2
toolX = (linkLength1 * math.cos(jointAngle1)
         + linkLength2 * math.cos(toolAngle))
toolY = (linkLength1 * math.sin(jointAngle1)
         + linkLength2 * math.sin(toolAngle))

print(f"TCP: ({toolX:.4f}, {toolY:.4f}) m")
print(f"Orientation: {math.degrees(toolAngle):.1f} deg")
```

Expected output:

```text
TCP: (0.3464, 0.5000) m
Orientation: 90.0 deg
```

## Sanity checks before trusting a model

- At $(\theta_1,\theta_2)=(0,0)$, the tool should be at $(a_1+a_2,0)$.
- At $(90^\circ,0)$, it should be at $(0,a_1+a_2)$.
- At $(0,180^\circ)$, it should be at $(a_1-a_2,0)$.
- Every position should satisfy the ideal radial workspace bound.

The outputs are desired or predicted geometry, not motor commands. This model contains no timing, obstacle checking, or torque calculation.

## Quick reference

| Quantity | Expression |
| --- | --- |
| Elbow position | $(a_1\cos\theta_1,a_1\sin\theta_1)$ |
| Link 2 absolute angle | $\theta_1+\theta_2$ |
| Tool position | Sum of both base-frame link displacements |
| Tool orientation | $\phi=\theta_1+\theta_2$ |

[Previous](01-coordinate-frames.md) · [Section index](README.md) · [Next: Inverse kinematics](03-inverse-kinematics.md)
