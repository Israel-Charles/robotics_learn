# Worked Solutions · Kinematics Foundations

Each exercise is repeated below so you can read its reasoning alongside the question. Attempt the [exercises](exercises.md) first.

## 1. Unit conversion

**Question.** Convert $45^\circ$ and $-90^\circ$ to radians.

**Solution.**

Apply $\theta_{\mathrm{rad}}=\theta_{\mathrm{deg}}\pi/180$:

$$
45\frac{\pi}{180}=\frac{\pi}{4}\text{ rad}\approx0.7854\text{ rad},
\qquad
-90\frac{\pi}{180}=-\frac{\pi}{2}\text{ rad}\approx-1.5708\text{ rad}.
$$

The sign is preserved: negative angles indicate clockwise rotation in our convention.

## 2. Frame transformation

**Question.** Frame B is rotated $90^\circ$ relative to A, with B's origin at $(0.5,0.2)$ m in A. A point has B-frame coordinates $(0.1,0.2)$ m. Find its A-frame coordinates, then recover the B-frame coordinates using the inverse mapping.

**Solution.**

At $90^\circ$, the frame rotation and translation are

$$
R=\begin{bmatrix}0&-1\\1&0\end{bmatrix},\qquad
 t=\begin{bmatrix}0.5\\0.2\end{bmatrix}\text{ m}.
$$

Apply $p^A=Rp^B+t$, multiplying each row by the coordinate column:

$$
p^A=\begin{bmatrix}0(0.1)-1(0.2)\\1(0.1)+0(0.2)\end{bmatrix}
+\begin{bmatrix}0.5\\0.2\end{bmatrix}
=\begin{bmatrix}-0.2+0.5\\0.1+0.2\end{bmatrix}
=\begin{bmatrix}0.3\\0.3\end{bmatrix}\text{ m}.
$$

For the inverse, subtract the translation before applying the transpose rotation:

$$
p^B=R^T(p^A-t)
=\begin{bmatrix}0&1\\-1&0\end{bmatrix}
\begin{bmatrix}0.3-0.5\\0.3-0.2\end{bmatrix}
=\begin{bmatrix}0.1\\0.2\end{bmatrix}\text{ m}.
$$

This recovers the original coordinates and checks both rotation direction and translation order.

## 3. Forward kinematics

**Question.** For $a_1=0.4$ m, $a_2=0.3$ m, $\theta_1=90^\circ$, and $\theta_2=-90^\circ$, find the elbow position, tool position, and tool orientation.

**Solution.**

Find the elbow first:

$$
x_e=0.4\cos90^\circ=0,\qquad y_e=0.4\sin90^\circ=0.4\text{ m}.
$$

The second link's absolute angle is $\theta_1+\theta_2=90^\circ-90^\circ=0^\circ$. Add its base-frame displacement:

$$
x=0+0.3\cos0^\circ=0.3\text{ m},\qquad
y=0.4+0.3\sin0^\circ=0.4\text{ m}.
$$

The elbow is $(0,0.4)$ m, the TCP is $(0.3,0.4)$ m, and the aligned tool orientation is $\phi=0^\circ$. Its radius is $\sqrt{0.3^2+0.4^2}=0.5$ m, which lies within $[0.1,0.7]$ m.

## 4. Inverse kinematics

**Question.** For $a_1=0.4$ m, $a_2=0.3$ m, and target $(0.3,0.4)$ m, find both elbow branches and their tool orientations. Verify both by forward kinematics.

**Solution.**

First check the target radius:

$$
r=\sqrt{0.3^2+0.4^2}=\sqrt{0.25}=0.5\text{ m}.
$$

It lies between $|0.4-0.3|=0.1$ m and $0.4+0.3=0.7$ m. Solve for the elbow cosine:

$$
c_2=\frac{0.09+0.16-0.16-0.09}{2(0.4)(0.3)}=\frac{0}{0.24}=0.
$$

Then $s_2=\pm\sqrt{1-0^2}=\pm1$, giving $\theta_2=\pm90^\circ$. The target direction is $\beta=\operatorname{atan2}(0.4,0.3)=53.1301^\circ$.

For the positive branch:

$$
\gamma_+=\operatorname{atan2}(0.3,0.4)=36.8699^\circ,\qquad
\theta_{1+}=53.1301^\circ-36.8699^\circ=16.2602^\circ.
$$

For the negative branch:

$$
\gamma_-=\operatorname{atan2}(-0.3,0.4)=-36.8699^\circ,\qquad
\theta_{1-}=53.1301^\circ-(-36.8699^\circ)=90^\circ.
$$

Add the joint angles to find tool orientation:

| Branch | $\theta_1$ | $\theta_2$ | $\phi$ |
| --- | --- | --- | --- |
| Positive elbow sine | $16.2602^\circ$ | $90^\circ$ | $106.2602^\circ$ |
| Negative elbow sine | $90^\circ$ | $-90^\circ$ | $0^\circ$ |

Check the positive branch in the forward equations:

$$
\begin{aligned}
x&=0.4\cos16.2602^\circ+0.3\cos106.2602^\circ
\approx0.384-0.084=0.300\text{ m},\\
y&=0.4\sin16.2602^\circ+0.3\sin106.2602^\circ
\approx0.112+0.288=0.400\text{ m}.
\end{aligned}
$$

Check the negative branch separately:

$$
x=0.4\cos90^\circ+0.3\cos0^\circ=0.3\text{ m},\qquad
y=0.4\sin90^\circ+0.3\sin0^\circ=0.4\text{ m}.
$$

Both produce the target position, with different orientations. Use unrounded angles to compute numerical residuals.

## 5. Unreachable target

**Question.** For $a_1=0.4$ m and $a_2=0.3$ m, calculate $c_2$ for target $(0.8,0)$ m. Explain why there is no real IK solution.

**Solution.**

$$
c_2=\frac{0.8^2-0.4^2-0.3^2}{0.24}
=\frac{0.39}{0.24}=1.625.
$$

No real angle has this cosine. Equivalently, the target radius 0.8 m exceeds the total link length of 0.7 m. This is not a small rounding error and must not be hidden by numerical clamping.

## 6. Apply limits

**Question.** For $a_1=0.4$ m, $a_2=0.3$ m, and target $(0.4,0.3)$ m, suppose joint 1 must lie between $-45^\circ$ and $45^\circ$, and joint 2 between $-120^\circ$ and $120^\circ$. Which branch from the lesson survives? Does that prove a collision-free path exists?

**Solution.**

At this target, $c_2=(0.16+0.09-0.16-0.09)/0.24=0$, so $\theta_2=\pm90^\circ$. The target direction is $36.8699^\circ$.

For $\theta_2=90^\circ$, subtract $\operatorname{atan2}(0.3,0.4)=36.8699^\circ$, giving $\theta_1=0^\circ$. For $\theta_2=-90^\circ$, subtract $-36.8699^\circ$, giving $\theta_1=73.7398^\circ$.

| Candidate | Joint 1 check | Joint 2 check | Result |
| --- | --- | --- | --- |
| $(0^\circ,90^\circ)$ | $-45\leq0\leq45$ | $-120\leq90\leq120$ | Passes both limits |
| $(73.7398^\circ,-90^\circ)$ | $73.7398>45$ | $-120\leq-90\leq120$ | Rejected by joint 1 limit |

Adding or subtracting $360^\circ$ from the rejected shoulder angle cannot bring it into $[-45^\circ,45^\circ]$. Only the first branch survives. This establishes a joint-limit-feasible endpoint, not a clear path: the current configuration, obstacles, and intermediate motion must also be checked.

## 7. Exceptional geometry

**Question.** If $a_1=a_2=0.3$ m, explain how the tool can stay at the base while the shoulder angle changes. What happens to tool orientation?

**Solution.**

Set the relative elbow angle to $180^\circ$. With equal link lengths $a=0.3$ m:

$$
x=a\cos\theta_1+a\cos(\theta_1+180^\circ),\qquad
y=a\sin\theta_1+a\sin(\theta_1+180^\circ).
$$

Use $\cos(a+180^\circ)=-\cos a$ and $\sin(a+180^\circ)=-\sin a$:

$$
x=a\cos\theta_1-a\cos\theta_1=0,\qquad
y=a\sin\theta_1-a\sin\theta_1=0.
$$

This cancellation holds for every shoulder angle. The position remains at the base, while the aligned tool orientation is $\phi=\theta_1+180^\circ$ modulo $360^\circ$. At shoulder angles $0^\circ$ and $90^\circ$, for example, the tool points at $180^\circ$ and $270^\circ$ respectively. This is an ideal geometric result that ignores link thickness and self-collision.

## 8. Mini-lab

**Question.** Using $a_1=0.4$ m and $a_2=0.3$ m, adapt the forward-kinematics Python example to evaluate $(0^\circ,0^\circ)$, $(90^\circ,0^\circ)$, $(0^\circ,180^\circ)$, and $(30^\circ,60^\circ)$. Record position, orientation, and distance from the base for each. Explain any tiny values near zero in the numerical output.

**Solution.**

For link lengths 0.4 m and 0.3 m:

| $\theta_1$ | $\theta_2$ | $x$ (m) | $y$ (m) | $\phi$ (degrees) | Radius (m) |
| --- | --- | --- | --- | --- | --- |
| 0° | 0° | 0.7000 | 0.0000 | 0 | 0.7000 |
| 90° | 0° | 0.0000 | 0.7000 | 90 | 0.7000 |
| 0° | 180° | 0.1000 | 0.0000 | 180 | 0.1000 |
| 30° | 60° | 0.3464 | 0.5000 | 90 | 0.6083 |

Calculate radius with `math.hypot(toolX, toolY)`. Each radius lies in $[0.1,0.7]$ m. Tiny nonzero values such as $10^{-17}$ m can appear because floating-point representations of angles and trigonometric calculations are approximate. Compare numerical results with a suitable tolerance rather than exact equality to zero.

Here is a complete implementation of the requested calculation:

```python
import math

linkLength1 = 0.4
linkLength2 = 0.3
jointAnglePairsDegrees = [(0, 0), (90, 0), (0, 180), (30, 60)]

for shoulderDegrees, elbowDegrees in jointAnglePairsDegrees:
    shoulderAngle = math.radians(shoulderDegrees)
    elbowAngle = math.radians(elbowDegrees)
    toolAngle = shoulderAngle + elbowAngle
    toolX = (linkLength1 * math.cos(shoulderAngle)
             + linkLength2 * math.cos(toolAngle))
    toolY = (linkLength1 * math.sin(shoulderAngle)
             + linkLength2 * math.sin(toolAngle))
    toolRadius = math.hypot(toolX, toolY)
    print(f"({shoulderDegrees}, {elbowDegrees}) deg: "
          f"TCP=({toolX:.4f}, {toolY:.4f}) m, "
          f"orientation={math.degrees(toolAngle):.1f} deg, "
          f"radius={toolRadius:.4f} m")
```

For the last row, $x\approx0.346410$ m and $y=0.5$ m, so $r=\sqrt{0.346410^2+0.5^2}\approx\sqrt{0.37}=0.6083$ m. This checks the radius independently of the code.

## 9. Velocity mapping

**Question.** For $a_1=0.4$ m, $a_2=0.3$ m, $\theta_1=0$, and $\theta_2=\pi/2$, calculate the position Jacobian. Find tool velocity for joint rates $(0.2,-0.1)$ rad/s, then find joint rates that produce tool velocity $(0,0.04)$ m/s at that configuration.

**Solution.** With $\sin0=0$, $\cos0=1$, $\sin(\pi/2)=1$, and $\cos(\pi/2)=0$, substitution gives

$$
J=\begin{bmatrix}-0.4(0)-0.3(1)&-0.3(1)\\0.4(1)+0.3(0)&0.3(0)\end{bmatrix}
=\begin{bmatrix}-0.3&-0.3\\0.4&0\end{bmatrix}.
$$

Multiplication gives $\dot x=-0.3(0.2)-0.3(-0.1)=-0.03$ m/s and $\dot y=0.4(0.2)=0.08$ m/s.

For the inverse request, solve the vertical equation first: $0.4\dot\theta_1=0.04$, so $\dot\theta_1=0.1$ rad/s. The horizontal equation is $-0.3\dot\theta_1-0.3\dot\theta_2=0$, hence $\dot\theta_2=-0.1$ rad/s. Substitution yields $(0,0.04)$ m/s as required. This rate pair must be recomputed as configuration changes.

## 10. Singular motion

**Question.** For the same positive link lengths, use $\det J=a_1a_2\sin\theta_2$ to identify singular elbow angles. At $\theta_1=\theta_2=0$, can joint motion produce horizontal tool velocity 0.01 m/s? Give two joint-rate pairs producing vertical velocity 0.07 m/s and explain whether a physical joint has lost its freedom.

**Solution.** Since $a_1a_2=0.12$ m² is nonzero, the determinant is zero exactly when $\sin\theta_2=0$. Thus $\theta_2=n\pi$ for integer $n$: straight or fully folded configurations, subject to joint limits.

At the specified straight configuration,

$$
J=\begin{bmatrix}0&0\\0.7&0.3\end{bmatrix}.
$$

The horizontal equation is $\dot x=0$ for every finite joint-rate pair, so 0.01 m/s horizontally is impossible at that instant. For vertical motion, $0.7\dot\theta_1+0.3\dot\theta_2=0.07$. Two solutions are $(0.1,0)$ and $(0,0.07/0.3)=(0,0.2333\ldots)$ rad/s. Both joints can still rotate; their effects on the position task span only one independent direction.

[Exercises](exercises.md) · [Section index](README.md) · [Next section](../04-control-and-interaction/README.md)
