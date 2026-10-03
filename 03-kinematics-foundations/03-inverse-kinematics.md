# Inverse Kinematics of a Planar Arm

**Inverse kinematics (IK)** finds joint configurations that produce a desired tool position or pose. Unlike forward kinematics, the result may contain no solution, one solution, several discrete solutions, or a continuous family.

We solve the two-link **position** problem: the inputs are link lengths $L_1,L_2$ and a desired tip location $(x,y)$; the unknowns are shoulder angle $\theta_1$ and relative elbow angle $\theta_2$.

Both links point along positive $x$ when their joint angles are zero, and positive angles turn counterclockwise. The tool is at link 2's tip and points along that link, exactly as in [Forward kinematics](02-forward-kinematics.md).

We are asking “Which joint angles place the tip here?” Once a pair of joint angles is found, its tool orientation follows as $\phi=\theta_1+\theta_2$. If an application specifies a required orientation, we must check it afterward; a position solution may fail that extra requirement.

## Step 1: Solve for the relative elbow angle

Start from the forward-position equations:

$$
x=L_1\cos\theta_1+L_2\cos(\theta_1+\theta_2),\qquad
y=L_1\sin\theta_1+L_2\sin(\theta_1+\theta_2).
$$

Square each expression using $(a+b)^2=a^2+2ab+b^2$, then add:

$$
\begin{aligned}
x^2+y^2={}&L_1^2(\cos^2\theta_1+\sin^2\theta_1)\\
&+L_2^2\bigl(\cos^2(\theta_1+\theta_2)+\sin^2(\theta_1+\theta_2)\bigr)\\
&+2L_1L_2\bigl(\cos\theta_1\cos(\theta_1+\theta_2)
+\sin\theta_1\sin(\theta_1+\theta_2)\bigr).
\end{aligned}
$$

Use $\cos^2 a+\sin^2 a=1$ for the first two parentheses. For the last, use $\cos(a-b)=\cos a\cos b+\sin a\sin b$ with $a=\theta_1+\theta_2$ and $b=\theta_1$. This leaves

$$
x^2+y^2=L_1^2+L_2^2+2L_1L_2\cos\theta_2.
$$

$$
\cos\theta_2=\frac{x^2+y^2-L_1^2-L_2^2}{2L_1L_2}=c_2.
$$

The symbol $c_2$ is shorthand for the elbow cosine, not another unknown angle. A real angle's cosine lies between $-1$ and $1$, so a position solution requires $-1\leq c_2\leq1$. Equivalently,

$$
(L_1-L_2)^2\leq x^2+y^2\leq(L_1+L_2)^2,
$$

which gives the radial workspace bound after taking square roots.

To obtain the sine, use $\sin^2\theta_2+\cos^2\theta_2=1$:

$$
\sin^2\theta_2=1-c_2^2,\qquad s_2=\sin\theta_2=\pm\sqrt{1-c_2^2}.
$$

Both signs must be considered: positive and negative elbow angles can have the same cosine. Recover the angle from its sine and cosine using

$$
\theta_2=\operatorname{atan2}(s_2,c_2).
$$

The two signs correspond to distinct elbow configurations, often called elbow-up and elbow-down. Which label belongs to which sign depends on the viewing and coordinate conventions; the signed angles are unambiguous here.

The function $\operatorname{atan2}(y,x)$ computes an angle using both components to identify the quadrant. Ordinary $\arctan(y/x)$ loses quadrant information and fails when the denominator is zero.

## Step 2: Solve for the shoulder angle

In a frame rotated with link 1, the base-to-tool vector has components

$$
\begin{bmatrix}L_1+L_2c_2\\L_2s_2\end{bmatrix}.
$$

Its angle in that frame is $\operatorname{atan2}(L_2s_2,L_1+L_2c_2)$. Subtract this from the target's base-frame angle:

$$
\boxed{\theta_1=\operatorname{atan2}(y,x)
-\operatorname{atan2}(L_2s_2,L_1+L_2c_2).}
$$

To see why this is a subtraction, call the target's base-frame direction $\beta=\operatorname{atan2}(y,x)$ and its direction relative to link 1 $\gamma=\operatorname{atan2}(L_2s_2,L_1+L_2c_2)$. Rotating the link-1 frame by $\theta_1$ gives $\beta=\theta_1+\gamma$, so $\theta_1=\beta-\gamma$ (up to equivalent full turns).

Apply this formula separately for each sign of $s_2$.

## Worked example: two solutions for one position

Take $L_1=0.4$ m, $L_2=0.3$ m and target $(x,y)=(0.4,0.3)$ m.

$$
c_2=\frac{0.4^2+0.3^2-0.4^2-0.3^2}{2(0.4)(0.3)}=0.
$$

Thus $s_2=\pm1$ and $\theta_2=\pm90^\circ$. The target direction is $\beta=\operatorname{atan2}(0.3,0.4)=36.8699^\circ$.

For $s_2=+1$, $\gamma=\operatorname{atan2}(0.3,0.4)=36.8699^\circ$, so $\theta_1=36.8699^\circ-36.8699^\circ=0^\circ$.

For $s_2=-1$, $\gamma=\operatorname{atan2}(-0.3,0.4)=-36.8699^\circ$, so $\theta_1=36.8699^\circ-(-36.8699^\circ)=73.7398^\circ$.

| Branch | $\theta_1$ | $\theta_2$ | Tool orientation $\phi$ |
| --- | --- | --- | --- |
| $s_2=+1$ | $0^\circ$ | $90^\circ$ | $90^\circ$ |
| $s_2=-1$ | $73.7398^\circ$ | $-90^\circ$ | $-16.2602^\circ$ |

For the first branch, the first link ends at $(0.4,0)$ m and the second link points upward by 0.3 m. For the second branch, the first link ends at approximately $(0.112,0.384)$ m and the second adds $(0.288,-0.084)$ m. Both arrive at $(0.4,0.3)$ m.

Their orientations differ. If the task also requires $\phi=0^\circ$, neither branch satisfies it. Reaching a point and achieving a pose are different problems.

## Boundary and exceptional cases

- At $c_2=1$, the links align and the two elbow branches coincide.
- At $c_2=-1$, the links are fully folded. Angles $+\pi$ and $-\pi$ describe the same relative link orientation, modulo a full turn.
- If $L_1=L_2$ and the target is the origin, any shoulder angle with a fully folded elbow places the tip at the origin. This gives a continuous family, and the shoulder formula encounters undefined zero-vector angles. Treat it separately.
- Floating-point arithmetic may produce a value just outside $[-1,1]$ for a boundary target. Check against a justified small numerical tolerance before clamping. Clamping a substantially invalid value would hide an unreachable target.

## Turn geometric solutions into candidates

After calculating IK:

1. Substitute each candidate into forward kinematics and measure the position error.
2. Check any tool-orientation requirement.
3. Account for equivalent angles and actual joint travel limits.
4. Check self-collision, obstacles, and other task constraints.
5. Prefer a feasible candidate suitable for the current configuration and motion plan.

An endpoint solution is not a safe or executable trajectory by itself. The entire path, speed, acceleration, and physical operating constraints still need consideration.

## Quick reference

| Step | Calculation |
| --- | --- |
| Elbow cosine | $c_2=(x^2+y^2-L_1^2-L_2^2)/(2L_1L_2)$ |
| Reachability | Require $c_2\in[-1,1]$ |
| Elbow branches | $s_2=\pm\sqrt{1-c_2^2}$ |
| Elbow angle | $\theta_2=\operatorname{atan2}(s_2,c_2)$ |
| Shoulder angle | $\theta_1=\operatorname{atan2}(y,x)-\operatorname{atan2}(L_2s_2,L_1+L_2c_2)$ |
| Verification | Evaluate forward kinematics for each candidate |

[Previous](02-forward-kinematics.md) · [Section index](README.md) · [Next: Velocity kinematics](04-velocity-kinematics.md)
