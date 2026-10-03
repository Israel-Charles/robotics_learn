# Velocity Kinematics and the Jacobian

Forward kinematics answers where the tool is. **Velocity kinematics** answers how fast and in which direction it moves when the joints move. We use the same planar 2R arm and base frame as the [forward model](02-forward-kinematics.md).

## Differentiate the position equations

A dot means a time derivative: $\dot\theta_1$ is shoulder angular velocity in rad/s, while $\dot x$ is horizontal tool velocity in m/s. Use radians when differentiating trigonometric functions.

The chain rule states that $d(\cos a)/dt=-\sin(a)\dot a$ and $d(\sin a)/dt=\cos(a)\dot a$. The angle $\theta_1+\theta_2$ changes at rate $\dot\theta_1+\dot\theta_2$. Thus

$$
\dot x=-L_1\sin\theta_1\dot\theta_1
-L_2\sin(\theta_1+\theta_2)(\dot\theta_1+\dot\theta_2),
$$

$$
\dot y=L_1\cos\theta_1\dot\theta_1
+L_2\cos(\theta_1+\theta_2)(\dot\theta_1+\dot\theta_2).
$$

Collect the coefficient of each joint velocity:

$$
\begin{bmatrix}\dot x\\\dot y\end{bmatrix}
=\underbrace{\begin{bmatrix}
-L_1\sin\theta_1-L_2\sin(\theta_1+\theta_2)&-L_2\sin(\theta_1+\theta_2)\\
L_1\cos\theta_1+L_2\cos(\theta_1+\theta_2)&L_2\cos(\theta_1+\theta_2)
\end{bmatrix}}_{J(q)}
\begin{bmatrix}\dot\theta_1\\\dot\theta_2\end{bmatrix}.
$$

The **Jacobian** $J(q)$ is the local joint-to-tool velocity map. Its first column is the tool velocity produced by unit shoulder rate with zero elbow rate. Its second column gives the effect of unit elbow rate with zero shoulder rate. Adding the scaled columns gives the combined motion.

## Worked example

Let $L_1=0.4$ m, $L_2=0.3$ m, $\theta_1=0$, and $\theta_2=\pi/2$. Then

$$
J=\begin{bmatrix}-0.3&-0.3\\0.4&0\end{bmatrix}.
$$

For joint rates $\dot\theta_1=0.2$ rad/s and $\dot\theta_2=-0.1$ rad/s:

$$
\dot x=-0.3(0.2)-0.3(-0.1)=-0.03\text{ m/s},\qquad
\dot y=0.4(0.2)=0.08\text{ m/s}.
$$

The tool moves left and upward. Its speed is $\sqrt{(-0.03)^2+0.08^2}\approx0.0854$ m/s. For an aligned tool, $\dot\phi=\dot\theta_1+\dot\theta_2=0.1$ rad/s.

## Reverse the velocity problem

At this configuration, a desired velocity $(0,0.04)$ m/s requires $0.4\dot\theta_1=0.04$, so $\dot\theta_1=0.1$ rad/s. The horizontal equation then requires $-0.3(0.1+\dot\theta_2)=0$, giving $\dot\theta_2=-0.1$ rad/s.

For a nonsingular square Jacobian, this is equivalent to $\dot q=J^{-1}\dot p$. It is an instantaneous calculation: update the Jacobian as configuration changes. Multiplying one velocity by a long time interval does not generally predict the full curved motion.

## Quick reference

- Position task: $\dot p=J(q)\dot q$.
- Planar pose task: append the row $[1\;1]$ to include $\dot\phi$; the resulting Jacobian is $3\times2$.
- More requested velocity components do not create more independent joints.
- A joint speed limit is not a configuration-independent TCP speed limit.

[Previous](03-inverse-kinematics.md) · [Section index](README.md) · [Next: Singularities](05-jacobians-and-singularities.md)
