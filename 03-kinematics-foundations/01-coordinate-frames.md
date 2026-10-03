# Coordinate Frames and Planar Transformations

## Coordinates need a reference

Saying “the object is at $(0.2,0.1)$ m” is incomplete unless we know the origin and axis directions. A **coordinate frame** supplies that reference.

A robot may use a world frame, a base frame, frames attached to links, a tool frame, and a camera frame. The same physical point generally has different coordinates in each.

In this section, use right-handed planar frames: $x$ points right, $y$ points up, and positive rotation is counterclockwise when viewed from positive $z$ toward the plane. Angles in formulas and code use radians unless marked with a degree symbol.

$$
\theta_{\mathrm{rad}}=\theta_{\mathrm{deg}}\frac{\pi}{180}.
$$

## Rotate a vector

Let frame B be rotated counterclockwise by $\theta$ relative to A. To express a B-frame vector in A, first express **B's two unit axis vectors** in A.

A unit vector along B's $x$ axis makes angle $\theta$ with A's $x$ axis. Its horizontal and vertical projections are $\cos\theta$ and $\sin\theta$:

$$
{}^A\hat{e}_{x_B}=\begin{bmatrix}\cos\theta\\\sin\theta\end{bmatrix}.
$$

B's $y$ axis is another $90^\circ$ counterclockwise, so its projections are

$$
{}^A\hat{e}_{y_B}
=\begin{bmatrix}\cos(\theta+90^\circ)\\\sin(\theta+90^\circ)\end{bmatrix}
=\begin{bmatrix}-\sin\theta\\\cos\theta\end{bmatrix}.
$$

In radians, the quarter turn is $\pi/2$. A vector whose B coordinates are $(u,v)$ consists of $u$ copies of B's $x$ unit vector plus $v$ copies of B's $y$ unit vector. Therefore its A coordinates are

$$
u\begin{bmatrix}\cos\theta\\\sin\theta\end{bmatrix}
+v\begin{bmatrix}-\sin\theta\\\cos\theta\end{bmatrix}.
$$

Placing these unit vectors in the two matrix columns packages that weighted sum as

$$
{}^A R_B=
\begin{bmatrix}
\cos\theta & -\sin\theta \\
\sin\theta & \cos\theta
\end{bmatrix}.
$$

The first column tells us where B's $x$ axis points in A; the second does the same for B's $y$ axis. Each entry is the dot product of a unit axis from A with a unit axis from B: $R_{ij}=\hat e_{i_A}\cdot\hat e_{j_B}$. A dot product of unit vectors equals the cosine of their included angle, so these entries are called **direction cosines**. The minus sign follows from the second axis's direction.

For a vector with components $[u,v]^T$ in B, multiplication gives

$$
{}^A R_B
\begin{bmatrix}u\\v\end{bmatrix}
=
\begin{bmatrix}
u\cos\theta-v\sin\theta\\
u\sin\theta+v\cos\theta
\end{bmatrix}.
$$

Each output component is the dot product of a matrix row with the input column. At $\theta=90^\circ$, the vector $[1,0]^T$ becomes $[0,1]^T$: B's positive $x$ direction points along A's positive $y$ direction.

## Locate a point with rotation and translation

Let $p^B$ be a point's coordinates in B. Let $t^A_B$ be the coordinates of B's origin in A. Then

$$
p^A = {}^A R_B p^B + t^A_B.
$$

For example, B is rotated $90^\circ$ and its origin lies at $(1,2)$ m in A. A point is at $(0.3,0)$ m in B. Its A-frame coordinates are

$$
p^A=
\begin{bmatrix}0&-1\\1&0\end{bmatrix}
\begin{bmatrix}0.3\\0\end{bmatrix}
+
\begin{bmatrix}1\\2\end{bmatrix}
=
\begin{bmatrix}1\\2.3\end{bmatrix}\text{ m}.
$$

The local displacement is rotated before adding the base-frame translation. Adding unconverted coordinates from different frames gives the wrong geometry.

To reverse this mapping:

$$
p^B=({}^A R_B)^T(p^A-t^A_B).
$$

A rotation matrix's transpose is its inverse. Subtract the translation first, then express the resulting displacement in B.

## Homogeneous transformations

A homogeneous transform combines both operations into one matrix:

$$
{}^A T_B=
\begin{bmatrix}
\cos\theta&-\sin\theta&t_x\\
\sin\theta&\cos\theta&t_y\\
0&0&1
\end{bmatrix},
\qquad
\begin{bmatrix}p_x^A\\p_y^A\\1\end{bmatrix}
={}^A T_B
\begin{bmatrix}p_x^B\\p_y^B\\1\end{bmatrix}.
$$

For an additional frame C:

$$
{}^A T_C={}^A T_B\,{}^B T_C.
$$

The rightmost transform acts first. Matrix order matters: rotating a translated point and translating a rotated point generally produce different locations.

For three-dimensional motion, the same structure uses a $3\times3$ rotation matrix inside a $4\times4$ homogeneous transform. We will keep the calculations planar here.

## Checkpoint

In the worked example, what are the B-frame coordinates of the point $(1,2.3)$ m expressed in A?

Subtracting $(1,2)$ gives $(0,0.3)$ m in A. Rotating by $-90^\circ$ yields $(0.3,0)$ m in B, recovering the original point.

## Quick reference

| Operation | Formula |
| --- | --- |
| Degrees to radians | $\theta_{\mathrm{rad}}=\theta_{\mathrm{deg}}\pi/180$ |
| B point to A coordinates | $p^A={}^A R_Bp^B+t^A_B$ |
| A point to B coordinates | $p^B=({}^A R_B)^T(p^A-t^A_B)$ |
| Compose frame transforms | ${}^A T_C={}^A T_B{}^B T_C$ |

[Section index](README.md) · [Next: Forward kinematics](02-forward-kinematics.md)
