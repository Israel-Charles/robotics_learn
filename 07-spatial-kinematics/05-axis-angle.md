# Axis–Angle and Exponential Coordinates

Any three-dimensional proper rotation can be described as a single turn through angle $\theta$ about a unit axis $\hat{\mathbf k}$. The axis passes through the origin; a rotation about an offset line also needs a translation when describing point motion.

## Build a matrix from an axis and angle

For $\hat{\mathbf k}=(k_x,k_y,k_z)^T$, define the skew-symmetric matrix

$$
[\hat{\mathbf k}]_\times=
\begin{bmatrix}0&-k_z&k_y\\k_z&0&-k_x\\-k_y&k_x&0\end{bmatrix}.
$$

It packages the cross product: $[\hat{\mathbf k}]_\times\mathbf v=\hat{\mathbf k}\times\mathbf v$. **Rodrigues' formula** gives

$$
\boxed{R=I+\sin\theta[\hat{\mathbf k}]_\times+(1-\cos\theta)[\hat{\mathbf k}]_\times^2.}
$$

Equivalently, $R=\cos\theta I+(1-\cos\theta)\hat{\mathbf k}\hat{\mathbf k}^T+\sin\theta[\hat{\mathbf k}]_\times$. The component of a vector parallel to the axis stays fixed; its perpendicular component turns in a plane.

Another way to construct this rotation is to choose a matrix $S$ whose third column is $\hat{\mathbf k}$, then use $R=SR_z(\theta)S^T$. From right to left, express the vector in axes where $\hat{\mathbf k}$ is the $z$ direction, turn about that $z$, and convert back. For an axis $\hat{\mathbf k}=(\cos u\sin v,\sin u\sin v,\cos v)^T$, choose $S=R_z(u)R_y(v)$. The resulting five-factor product is $R_z(u)R_y(v)R_z(\theta)R_y(-v)R_z(-u)$.

For $\hat{\mathbf k}=(0,0,1)^T$ and $\theta=90^\circ$, Rodrigues' formula gives $R_z(90^\circ)$. Applied to $(1,0,0)^T$, it produces $(0,1,0)^T$.

## Recover axis and angle

For a valid rotation matrix, select $0\le\theta\le\pi$:

$$
\theta=\arccos\left(\frac{\operatorname{tr}(R)-1}{2}\right).
$$

The trace is the sum of the diagonal entries. In numerical calculations, clamp the argument to $[-1,1]$ to accommodate tiny rounding errors; clamping does not make an arbitrary invalid matrix a rotation.

For $0<\theta<\pi$,

$$
\hat{\mathbf k}=\frac{1}{2\sin\theta}
\begin{bmatrix}r_{32}-r_{23}\\r_{13}-r_{31}\\r_{21}-r_{12}\end{bmatrix}.
$$

At $\theta=0$, $R=I$ and the axis is arbitrary. At $\theta=\pi$, division by $\sin\theta$ fails. Instead use

$$
\frac{R+I}{2}=\hat{\mathbf k}\hat{\mathbf k}^T.
$$

Choose its largest diagonal entry, say the $x$ entry. Set $k_x$ to its positive square root, then recover $k_y$ and $k_z$ by dividing the first column's remaining entries by $k_x$. Normalize the result. Use the corresponding column if $y$ or $z$ has the largest diagonal. Either overall sign describes the same half-turn. Near $0$ or $\pi$, use numerical routines with special branches instead of dividing by a very small sine.

## A three-component rotation vector

The **exponential coordinates** are $\mathbf r=\theta\hat{\mathbf k}$, with $\theta$ in radians. The magnitude specifies the angle and the direction specifies the axis:

$$
R=\exp([\mathbf r]_\times).
$$

The exponential acts on a **matrix**, not element by element on the three-vector. Its power series is $I+M+M^2/2!+\cdots$ for $M=[\mathbf r]_\times$; Rodrigues' formula evaluates this exponential for rotations. See [Modern Robotics on exponential coordinates](https://modernrobotics.northwestern.edu/nu-gm-book-resource/3-2-3-exponential-coordinates-of-rotation-part-2-of-2/).

For a $90^\circ$ turn about $z$, $\mathbf r=(0,0,\pi/2)^T$. In general, adding two rotation vectors does **not** compose their finite rotations: the corresponding matrices need not commute.

Axis–angle avoids Euler's particular three-axis sequence, but is not globally unique: $(\hat{\mathbf k},\theta)$ and $(-\hat{\mathbf k},-\theta)$ agree, and the axis at zero angle is undefined. The principal rotation vector also has an ambiguity at half-turns.

[Previous](04-euler-angles.md) · [Section index](README.md) · [Next: Unit quaternions](06-unit-quaternions.md)
