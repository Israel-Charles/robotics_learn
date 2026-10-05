# Spatial Homogeneous Transformations

A robot-mounted camera has both an orientation and an offset from the robot base. How do we express a detected point in the base frame?

## Combine rotation and translation

Let ${}^{A}\mathbf t_B$ be the position of frame $B$'s origin expressed in $A$. Then a point has coordinates

$$
{}^{A}\mathbf p={}^{A}R_B\,{}^{B}\mathbf p+{}^{A}\mathbf t_B.
$$

Adding a fourth coordinate turns this into one matrix multiplication:

$$
\begin{bmatrix}{}^{A}\mathbf p\\1\end{bmatrix}
=\underbrace{\begin{bmatrix}{}^{A}R_B&{}^{A}\mathbf t_B\\0\;0\;0&1\end{bmatrix}}_{{}^{A}T_B}
\begin{bmatrix}{}^{B}\mathbf p\\1\end{bmatrix}.
$$

This $4\times4$ **homogeneous transformation** represents a rigid pose. Such transforms form $SE(3)$, the special Euclidean group. Its rotation block must be in $SO(3)$; the translation is a three-vector. A general matrix with this last row is not necessarily rigid if its upper-left block scales or shears.

A free vector uses fourth coordinate **zero**:

$$
{}^{A}T_B\begin{bmatrix}{}^{B}\mathbf v\\0\end{bmatrix}
=\begin{bmatrix}{}^{A}R_B\,{}^{B}\mathbf v\\0\end{bmatrix}.
$$

Translation affects locations but not free directions. This rigid-body transform is different from a camera's projective homography, which maps image-plane coordinates and need not preserve lengths or angles.

### Worked example

Take ${}^{A}R_B=R_z(90^\circ)$ and ${}^{A}\mathbf t_B=(1,2,3)^T\ \mathrm m$. A point at ${}^{B}\mathbf p=(0.2,0,0)^T\ \mathrm m$ becomes $(1,2.2,3)^T\ \mathrm m$ in $A$. A displacement with the same three components becomes $(0,0.2,0)^T\ \mathrm m$ instead.

## Compose frame chains

$$
{}^{A}T_C={}^{A}T_B\,{}^{B}T_C,
$$

so the blocks satisfy

$$
{}^{A}R_C={}^{A}R_B\,{}^{B}R_C,\qquad
{}^{A}\mathbf t_C={}^{A}R_B\,{}^{B}\mathbf t_C+{}^{A}\mathbf t_B.
$$

Translations cannot generally be added directly: they must first be expressed in the same frame. If $B$ is rotated $90^\circ$ about $A$'s $z$, its origin is $(1,0,0)^T\ \mathrm m$ in $A$, and $C$ is one metre along $B$'s $x$, then $C$'s origin is $(1,1,0)^T\ \mathrm m$ in $A$, not $(2,0,0)^T$.

## Invert a pose

$$
\boxed{T^{-1}=\begin{bmatrix}R^T&-R^T\mathbf t\\0\;0\;0&1\end{bmatrix}.}
$$

Undo translation and rotate coordinates back. The inverse translation must be expressed in the reversed destination frame; it is not generally just $-\mathbf t$. For the camera example above, it is $(-2,1,-3)^T\ \mathrm m$. Applying the inverse recovers the original point.

## Compose elementary motions

Write $\mathcal R_x(\alpha)$ for a $4\times4$ pure rotation and $\mathcal T_x(b)$ for a pure translation. Starting from alignment, turn about current $x$ by $\alpha$, move $b$ along current $x$, move $d$ along current $z$, then turn about current $z$ by $\theta$:

$$
T=\mathcal R_x(\alpha)\mathcal T_x(b)\mathcal T_z(d)\mathcal R_z(\theta).
$$

Its rotation is $R_x(\alpha)R_z(\theta)$ and its translation is $(b,-d\sin\alpha,d\cos\alpha)^T$. The last turn changes orientation about the current origin without moving that origin. This example specifies its own motion sequence; the **standard DH sequence** is defined in the next lesson.

[Previous](06-unit-quaternions.md) · [Section index](README.md) · [Next: Standard DH](08-denavit-hartenberg.md)
