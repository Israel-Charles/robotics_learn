# Spatial Kinematics: Worked Solutions

Attempt the [exercises](exercises.md) first. Matrix indices start at 1; all displayed numerical angles are in degrees unless written using $\pi$.

## 1. Rotation or reflection

**Question.** For $R=R_z(90^\circ)$, express $(1,2,3)^T$ in the rotated result and verify its length is unchanged. Explain why $\operatorname{diag}(1,1,-1)$ is not a proper rotation even though it also preserves length.

Multiplication gives $(-2,1,3)^T$. Both squared lengths are $1+4+9=14$. For $R$, $R^TR=I$ and $\det R=1$. The diagonal matrix is orthogonal but has determinant $-1$: it reflects across the $xy$ plane and reverses handedness.

## 2. Order and operator coordinates

**Question.** Starting from identity, compare current-$x$ then current-$y$ rotations of $90^\circ$ with fixed-$x$ then fixed-$y$ rotations of $90^\circ$, by applying each result to $(0,0,1)^T$. If ${}^{A}R_B=R_y(90^\circ)$, express an active rotation $Q_A=R_z(\delta)$ in frame $B$.

The current-axis sequence postmultiplies: $R_xR_y\mathbf e_z=R_x\mathbf e_x=\mathbf e_x$. The fixed-axis sequence premultiplies: $R_yR_x\mathbf e_z=R_y(-\mathbf e_y)=-\mathbf e_y$. All rotations in these two products are $90^\circ$.

Let $S={}^{A}R_B$. Change operator coordinates by $Q_B=S^TQ_AS=R_y(-90^\circ)R_z(\delta)R_y(90^\circ)=R_x(-\delta)$. The negative sign agrees with $S^T\mathbf e_z=-\mathbf e_x$: the positive $A$-$z$ axis points along negative $B$-$x$.

## 3. Roll–pitch–yaw branches

**Question.** Extract one roll–pitch–yaw triplet from $R=\begin{bmatrix}0&-1&0\\\sqrt3/2&0&1/2\\-1/2&0&\sqrt3/2\end{bmatrix}$, and give the second branch. Explain why $(20^\circ,90^\circ,50^\circ)$ and $(0^\circ,90^\circ,30^\circ)$ represent the same orientation without implying a mechanical singularity.

Using the principal extraction formulas gives $\rho=\operatorname{atan2}(0,\sqrt3/2)=0^\circ$, $\beta=\operatorname{atan2}(1/2,\sqrt3/2)=30^\circ$, and $\psi=\operatorname{atan2}(\sqrt3/2,0)=90^\circ$. The second branch is $(180^\circ,150^\circ,270^\circ)$, with equivalent wrapped angles allowed.

At pitch $90^\circ$, the orientation depends on $\rho-\psi$. Both supplied triplets give $-30^\circ$. Separate roll and yaw values are therefore not identifiable. This is a failure of local uniqueness in the angle coordinates; physical motion limitations depend on the robot's Jacobian, which has not been specified.

## 4. ZYZ extraction

**Question.** Recover a principal ZYZ triplet from $R=\begin{bmatrix}0&-1&0\\0&0&1\\-1&0&0\end{bmatrix}$. At middle angle $0^\circ$, give two outer-angle pairs that yield $R_z(60^\circ)$. At middle angle $180^\circ$, which combination of outer angles remains identifiable?

The extraction gives $\beta=\operatorname{atan2}(1,0)=90^\circ$, $\eta=\operatorname{atan2}(1,0)=90^\circ$, and $\gamma=\operatorname{atan2}(0,1)=0^\circ$. At $\beta=0$, the product reduces to $R_z(\eta+\gamma)$, so $(\eta,\gamma)=(20^\circ,40^\circ)$ and $(60^\circ,0^\circ)$ both work. At $\beta=180^\circ$, only $\eta-\gamma=\operatorname{atan2}(-r_{21},-r_{11})$ is identifiable, modulo complete turns.

## 5. Axis–angle limits

**Question.** Find a principal axis–angle description and rotation vector for $R=\operatorname{diag}(-1,-1,1)$. Explain why the antisymmetric-entry formula fails here and why adding arbitrary rotation vectors is not a general composition rule.

The trace is $-1$, so $\theta=\arccos(-1)=\pi$. Here $(R+I)/2=\operatorname{diag}(0,0,1)$, giving an axis $(0,0,1)^T$ and rotation vector $(0,0,\pi)^T$. Choosing the negative axis also represents the same half-turn.

The antisymmetric-entry formula would divide a zero vector by $2\sin\pi=0$. The symmetric half-turn formula avoids this undefined operation. Rotation-vector addition generally fails because rotations about different axes do not commute, whereas vector addition does.

## 6. Quaternion composition

**Question.** In scalar-last order, let $q=(0,0,\sqrt2/2,\sqrt2/2)$. Find $q\otimes q$, state its rotation, and find the result of rotating $(1,0,0)^T$ by $q$. Give the halfway SLERP orientation from identity to $q$, and explain whether $-q$ represents a different orientation.

The product has vector part $(0,0,2(\sqrt2/2)^2)=(0,0,1)$ and scalar part $1/2-1/2=0$. Thus $q\otimes q=(0,0,1,0)$ represents $180^\circ$ about $z$. The original $q$ rotates $(1,0,0)^T$ to $(0,1,0)^T$.

Halfway SLERP gives $(0,0,\sin22.5^\circ,\cos22.5^\circ)$, a $45^\circ$ turn about $z$. Negating all four components leaves the rotation unchanged; it changes the representative on the quaternion sphere.

## 7. Points, vectors, and inverse transforms

**Question.** Let ${}^{A}T_B$ have rotation $R_z(90^\circ)$ and translation $(1,2,3)^T\ \mathrm m$. Transform both a point and a displacement with $B$ coordinates $(0.2,0,0)^T\ \mathrm m$. Find the inverse translation and use the inverse transform to recover the original point.

The rotation maps the three components to $(0,0.2,0)^T$. Add translation for the point, giving $(1,2.2,3)^T\ \mathrm m$. The displacement stays $(0,0.2,0)^T\ \mathrm m$ because its fourth homogeneous coordinate is zero.

The inverse translation is $-R^T\mathbf t=(-2,1,-3)^T\ \mathrm m$. Apply the inverse to the point:

$$
R^T(1,2.2,3)^T+(-2,1,-3)^T
=(2.2,-1,3)^T+(-2,1,-3)^T=(0.2,0,0)^T\ \mathrm m.
$$

## 8. Local translation in a chain

**Question.** Let ${}^{A}T_B$ have rotation $R_z(90^\circ)$ and translation $(1,0,0)^T\ \mathrm m$. Let ${}^{B}T_C$ have identity rotation and translation $(1,0,0)^T\ \mathrm m$. Find ${}^{A}T_C$. Separately, find the translation of $\mathcal R_x(90^\circ)\mathcal T_x(0.2)\mathcal T_z(0.3)\mathcal R_z(45^\circ)$, with distances in metres.

The composed rotation is $R_z(90^\circ)$. Its translation is $R_z(90^\circ)(1,0,0)^T+(1,0,0)^T=(1,1,0)^T\ \mathrm m$, hence

$$
{}^{A}T_C=\begin{bmatrix}0&-1&0&1\\1&0&0&1\\0&0&1&0\\0&0&0&1\end{bmatrix},
$$

with translation entries in metres. The second expression has translation $R_x(90^\circ)(0.2,0,0.3)^T=(0.2,-0.3,0)^T\ \mathrm m$. The final local rotation leaves this origin unchanged.

## 9. DH and tool offsets

**Question.** For the planar arm with $a_1=0.4\ \mathrm m$, $a_2=0.3\ \mathrm m$, $\theta_1=30^\circ$, and $\theta_2=60^\circ$, give its standard DH table and compute frame 2's pose in frame 0. A tool is mounted $0.1\ \mathrm m$ along frame 2's positive $x$ with no relative rotation. Find the TCP position. Which parameter would vary for a prismatic DH joint?

| $i$ | $\theta_i$ | $d_i$ (m) | $a_i$ (m) | $\alpha_i$ |
| --- | --- | --- | --- | --- |
| 1 | $30^\circ$ | 0 | 0.4 | $0^\circ$ |
| 2 | $60^\circ$ | 0 | 0.3 | $0^\circ$ |

The adjacent transforms multiply to give $R_z(90^\circ)$ and position $(0.4\cos30^\circ+0.3\cos90^\circ,0.4\sin30^\circ+0.3\sin90^\circ,0)^T\approx(0.3464,0.5000,0)^T\ \mathrm m$.

The tool offset is expressed in frame 2, so rotate it before adding: $\mathbf p_{\mathrm{TCP}}=\mathbf p_2+R_z(90^\circ)(0.1,0,0)^T\approx(0.3464,0.6000,0)^T\ \mathrm m$. The tool orientation remains $R_z(90^\circ)$. A prismatic joint varies $d_i$; its $\theta_i$ stays fixed.

[Section index](README.md) · [Exercises](exercises.md)
