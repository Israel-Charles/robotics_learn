# Jacobians and Singularities

For the planar tool-position task, a singular configuration makes the two joint effects linearly dependent: they no longer provide two independent tool-velocity directions. This gives a mathematical version of the [tangent explanation](../02-manipulators-and-motion/03-workspace-and-limitations.md).

## Derive the singular configurations

For a $2\times2$ matrix $\begin{bmatrix}a&b\\c&d\end{bmatrix}$, the determinant is $ad-bc$. A zero determinant means the square matrix has no inverse.

Apply this to the [position Jacobian](04-velocity-kinematics.md), writing $s_1=\sin\theta_1$, $c_1=\cos\theta_1$, $s_{12}=\sin(\theta_1+\theta_2)$, and $c_{12}=\cos(\theta_1+\theta_2)$:

$$
\begin{aligned}
\det J
&=(-L_1s_1-L_2s_{12})L_2c_{12}
-(-L_2s_{12})(L_1c_1+L_2c_{12})\\
&=L_1L_2(s_{12}c_1-s_1c_{12})\\
&=L_1L_2\sin\theta_2.
\end{aligned}
$$

The $L_2^2s_{12}c_{12}$ terms cancel. The final step uses $\sin(a-b)=\sin a\cos b-\cos a\sin b$.

For positive link lengths, singularity therefore occurs when $\sin\theta_2=0$, or

$$
\theta_2=n\pi,\qquad n\text{ an integer}.
$$

Even multiples give straight alignment; odd multiples give full folding. Only configurations permitted by the actual joint limits are relevant to the real arm.

## Which velocity is missing?

At $\theta_1=\theta_2=0$ with lengths 0.4 m and 0.3 m:

$$
J=\begin{bmatrix}0&0\\0.7&0.3\end{bmatrix},\qquad
\dot x=0,\quad \dot y=0.7\dot\theta_1+0.3\dot\theta_2.
$$

No finite joint-rate pair produces a nonzero horizontal velocity at this instant. A vertical velocity of 0.07 m/s has many solutions, including $(0.1,0)$ rad/s and $(0,0.2333\ldots)$ rad/s. Losing an inverse does not mean that every requested motion is impossible.

Both joints still have their mechanical freedoms. The **rank of this task's velocity map** has fallen from two to one. Describing this as “the robot loses a DOF” without identifying the task can obscure that distinction.

## Near-singular and non-square cases

Near alignment, some desired velocities require large opposing joint rates. Check the resulting rates against actuator limits; slowing or changing the path may be necessary. A determinant is only defined for square matrices. For a general robot or task, examine rank relative to its ordinary maximum rather than applying a determinant test to a rectangular Jacobian.

The planar pose Jacobian has three rows and two columns, so arbitrary $\dot x,\dot y,\dot\phi$ cannot generally be prescribed together. Its rank properties need not match the two-row position Jacobian.

## Quick reference

For this 2R position model, $\det J=L_1L_2\sin\theta_2$. Singularities occur at straight or folded configurations and describe instantaneous task-motion capability. They do not remove a physical hinge or guarantee that all nearby finite motions are impossible.

[Previous](04-velocity-kinematics.md) · [Section index](README.md) · [Practice](exercises.md)
