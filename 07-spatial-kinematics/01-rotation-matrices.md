# Points, Vectors, and Rotation Matrices

How can a camera and robot base describe the same direction with different numbers?

## Geometry and coordinates

A **point** identifies a location. Its position coordinates depend on both the origin and axes of the chosen frame. A **free vector**, such as a displacement or force, has direction and magnitude but no fixed starting point. Changing the origin alone changes point coordinates but not free-vector coordinates.

For now, let frames $A$ and $B$ share an origin. Write a vector as a column, ${}^{B}\mathbf v=(v_x,v_y,v_z)^T$. Its coordinates in $A$ are

$$
{}^{A}\mathbf v={}^{A}R_B\,{}^{B}\mathbf v.
$$

The vector itself has not moved. We changed the axes used to describe it.

## Columns are frame axes

$$
{}^{A}R_B=
\begin{bmatrix}|&|&|\\ {}^{A}\hat{\mathbf x}_B&{}^{A}\hat{\mathbf y}_B&{}^{A}\hat{\mathbf z}_B\\ |&|&|\end{bmatrix}.
$$

Each column is a unit axis of $B$ expressed in $A$. Entry $r_{ij}$ is the dot product of axis $i$ of $A$ with axis $j$ of $B$: the cosine of the angle between them. This explains the name **direction cosine matrix**. Row $i$ collects the projections onto axis $i$ of $A$.

For example, if $B$ is turned $90^\circ$ about $A$'s positive $z$ axis,

$$
{}^{A}R_B=\begin{bmatrix}0&-1&0\\1&0&0\\0&0&1\end{bmatrix}.
$$

Its first column says that $B$'s positive $x$ points along $A$'s positive $y$. A vector with $B$ coordinates $(1,0,0)^T$ therefore has $A$ coordinates $(0,1,0)^T$.

## What makes a matrix a rotation?

The axes must be perpendicular unit vectors forming a right-handed frame:

$$
R^TR=I,\qquad \det R=+1,\qquad R^{-1}=R^T.
$$

Such matrices form $SO(3)$, the **special orthogonal group** in three dimensions. In the plane the corresponding group is $SO(2)$. “Orthogonal” expresses perpendicular unit axes; “special” excludes reflections, which have determinant $-1$.

Although $R$ has nine entries, unit-length and perpendicularity requirements impose six independent constraints, leaving three continuous rotational degrees of freedom. The determinant condition selects the proper-rotation component.

Rotations preserve dot products:

$$
(R\mathbf u)^T(R\mathbf v)=\mathbf u^TR^TR\mathbf v=\mathbf u^T\mathbf v.
$$

Consequently, lengths and angles are preserved. To reverse a coordinate conversion, use ${}^{B}R_A=({}^{A}R_B)^T$.

## Basic rotations

Let $c=\cos\theta$ and $s=\sin\theta$:

$$
R_x(\theta)=\begin{bmatrix}1&0&0\\0&c&-s\\0&s&c\end{bmatrix},\quad
R_y(\theta)=\begin{bmatrix}c&0&s\\0&1&0\\-s&0&c\end{bmatrix},\quad
R_z(\theta)=\begin{bmatrix}c&-s&0\\s&c&0\\0&0&1\end{bmatrix}.
$$

Point your right thumb along the positive rotation axis; your curled fingers give positive rotation. For example, $R_y(90^\circ)(0,1,1)^T=(1,1,0)^T$.

Here, if both vectors are expressed in the same fixed frame, the matrix **actively rotates** the vector. The same numerical matrix can instead describe a rotated frame and convert its coordinates to the fixed frame. State which operation is intended; converting fixed-frame coordinates into that rotated frame uses the transpose.

**Checkpoint:** Why is $\operatorname{diag}(1,1,-1)$ not a rotation? It preserves lengths but reverses handedness: its determinant is $-1$.

[Section index](README.md) · [Next: Rotation composition](02-rotation-composition.md)
