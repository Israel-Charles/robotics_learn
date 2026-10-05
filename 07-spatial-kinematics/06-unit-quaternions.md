# Unit Quaternions

Unit quaternions represent orientation compactly and support smooth interpolation without Euler-angle gimbal lock. They use four numbers with one constraint, so they still describe three rotational degrees of freedom.

## State the convention

We use **scalar-last** storage $q=(x,y,z,w)=(\mathbf v,w)$ and Hamilton multiplication. Some systems store $w$ first or use a different multiplication convention; verify both when exchanging data.

In algebraic notation the same quaternion is $w+xi+yj+zk$, where $i^2=j^2=k^2=-1$, $ij=k$, $jk=i$, and $ki=j$. Reversing any of these last three products changes its sign. This noncommutativity is reflected in quaternion rotation composition.

For unit axis $\hat{\mathbf k}$ and right-handed angle $\theta$,

$$
\mathbf v=\hat{\mathbf k}\sin(\theta/2),\qquad w=\cos(\theta/2),\qquad
x^2+y^2+z^2+w^2=1.
$$

The identity is $(0,0,0,1)$. A $90^\circ$ turn about $z$ is $(0,0,\sqrt2/2,\sqrt2/2)$. Both $q$ and $-q$ represent the same rotation: unit quaternions **double-cover** the set of orientations.

## Compose and invert

For $q_1=(\mathbf v_1,w_1)$ and $q_2=(\mathbf v_2,w_2)$,

$$
q_1\otimes q_2=
\left(w_1\mathbf v_2+w_2\mathbf v_1+\mathbf v_1\times\mathbf v_2,
w_1w_2-\mathbf v_1\cdot\mathbf v_2\right).
$$

With our convention, $R(q_1\otimes q_2)=R(q_1)R(q_2)$. For active vector rotations the rightmost rotation acts first. The inverse of a **unit** quaternion is its conjugate: $q^{-1}=(-\mathbf v,w)$.

To rotate a vector $\mathbf p$, treat it as $(\mathbf p,0)$ and evaluate $q\otimes(\mathbf p,0)\otimes q^{-1}$. The resulting vector part is the rotated vector and its scalar part is zero. Translation requires a separate position or homogeneous transform.

## Convert to and from a rotation matrix

Using the skew matrix from [axis–angle](05-axis-angle.md),

$$
R(q)=(w^2-\mathbf v^T\mathbf v)I+2\mathbf v\mathbf v^T+2w[\mathbf v]_\times.
$$

For the $90^\circ$ $z$ quaternion, this gives $\begin{bmatrix}0&-1&0\\1&0&0\\0&0&1\end{bmatrix}$, so $(1,0,0)^T$ rotates to $(0,1,0)^T$.

One inverse route is to recover the axis and angle using the preceding lesson, including its zero-angle and half-turn branches, and apply the half-angle formula. Away from $w=0$, a direct route is

$$
w=\tfrac12\sqrt{1+\operatorname{tr}R},\qquad
\mathbf v=\frac{1}{4w}(r_{32}-r_{23},\ r_{13}-r_{31},\ r_{21}-r_{12})^T.
$$

This selects $w\ge0$. It is unstable near a $180^\circ$ turn, where $w$ is near zero. Use the axis–angle special case or a largest-component conversion routine there. Normalize computed quaternions to remove small floating-point drift; a zero quaternion cannot be normalized and is not an orientation.

## Interpolate orientations

Given unit endpoints $q_0,q_1$, first negate $q_1$ if their four-dimensional dot product is negative. This chooses matching signs for the shorter arc. Let $\Omega=\arccos(q_0\cdot q_1)$ and interpolation fraction $0\le t\le1$:

$$
\operatorname{slerp}(q_0,q_1,t)=
\frac{\sin((1-t)\Omega)}{\sin\Omega}q_0+
\frac{\sin(t\Omega)}{\sin\Omega}q_1.
$$

For nearly equal endpoints, normalize $(1-t)q_0+tq_1$ to avoid division by a tiny sine. Clamp the dot product for rounding before applying $\arccos$. At a relative half-turn, either shortest direction needs a consistent choice.

For identity to $90^\circ$ about $z$, the halfway orientation is $45^\circ$ about $z$: $(0,0,\sin22.5^\circ,\cos22.5^\circ)$. Interpolating orientation alone does not establish collision freedom or joint feasibility; those belong to [motion planning](../04-control-and-interaction/02-position-paths-and-trajectories.md).

[Previous](05-axis-angle.md) · [Section index](README.md) · [Next: Homogeneous transformations](07-homogeneous-transformations.md)
