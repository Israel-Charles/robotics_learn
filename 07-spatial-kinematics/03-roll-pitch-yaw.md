# Roll, Pitch, and Yaw

Three angles are convenient for specifying a tool's orientation, but their names alone do not define a rotation. We must state the axes and order.

## Our convention

Use roll $\rho$ about $x$, pitch $\beta$ about $y$, and yaw $\psi$ about $z$. Starting from aligned frames, perform **fixed-axis $x$, then $y$, then $z$ rotations**:

$$
\boxed{R=R_z(\psi)R_y(\beta)R_x(\rho).}
$$

Equivalently, perform current-axis $z$, then $y$, then $x$ rotations by yaw, pitch, and roll. This uses three distinct axes, so it is a **Tait–Bryan** convention. Libraries sometimes use “Euler angles” for both Tait–Bryan and proper Euler sequences. Always check the full convention, angle units, and storage order.

Writing $c_\rho=\cos\rho$, $s_\rho=\sin\rho$, and similarly for the other angles:

$$
R=\begin{bmatrix}
c_\psi c_\beta&c_\psi s_\beta s_\rho-s_\psi c_\rho&c_\psi s_\beta c_\rho+s_\psi s_\rho\\
s_\psi c_\beta&s_\psi s_\beta s_\rho+c_\psi c_\rho&s_\psi s_\beta c_\rho-c_\psi s_\rho\\
-s_\beta&c_\beta s_\rho&c_\beta c_\rho
\end{bmatrix}.
$$

## Recover angles from a matrix

Let $r_{ij}$ mean row $i$, column $j$. Away from $\cos\beta=0$, one solution with $-\pi/2<\beta<\pi/2$ is

$$
\beta=\operatorname{atan2}\left(-r_{31},\sqrt{r_{11}^2+r_{21}^2}\right),\quad
\rho=\operatorname{atan2}(r_{32},r_{33}),\quad
\psi=\operatorname{atan2}(r_{21},r_{11}).
$$

Here $\operatorname{atan2}(y,x)$ uses both signs to choose a quadrant. The square root selects nonnegative $\cos\beta$. A second branch is $(\rho+\pi,\pi-\beta,\psi+\pi)$, with angles wrapped as desired. Adding complete turns also leaves the orientation unchanged.

### Worked example

For roll $0^\circ$, pitch $30^\circ$, yaw $90^\circ$,

$$
R=\begin{bmatrix}0&-1&0\\\sqrt3/2&0&1/2\\-1/2&0&\sqrt3/2\end{bmatrix}.
$$

Extraction gives $\beta=\operatorname{atan2}(1/2,\sqrt3/2)=30^\circ$, $\rho=0^\circ$, and $\psi=90^\circ$. Another valid triplet is $(180^\circ,150^\circ,270^\circ)$. Substitute either into the forward formula to verify it.

## Why gimbal lock occurs

At $\beta=+90^\circ$, the matrix depends on roll and yaw only through $\rho-\psi$. At $\beta=-90^\circ$, it depends only on $\rho+\psi$. Two angle changes can then describe the same orientation change, so roll and yaw cannot be recovered separately. This is a **coordinate singularity**, commonly called gimbal lock.

For example, $(\rho,\beta,\psi)=(20^\circ,90^\circ,50^\circ)$ and $(0^\circ,90^\circ,30^\circ)$ describe the same orientation. At either singular pitch, one valid convention is to set $\rho=0$ and choose $\psi=\operatorname{atan2}(-r_{12},r_{22})$.

The orientation still exists and its rotation matrix remains invertible. The angle description has lost local uniqueness. This does **not**, by itself, mean a robot mechanism has lost a physical motion direction; that requires examining its [Jacobian](../03-kinematics-foundations/05-jacobians-and-singularities.md).

Near this singularity, small orientation changes can produce large changes in extracted angles. Direct angle interpolation also encounters wrapping: averaging $179^\circ$ and $-179^\circ$ produces $0^\circ$, although the orientations are close. Use a suitable rotation interpolation method, such as the quaternion method in [Lesson 06](06-unit-quaternions.md).

[Previous](02-rotation-composition.md) · [Section index](README.md) · [Next: Proper Euler angles](04-euler-angles.md)
