# Proper Euler Angles

Proper Euler angles use a repeated first and third axis, such as $ZYZ$ or $ZXZ$. This differs from the three distinct axes of a Tait–Bryan sequence. Either family can be described with intrinsic or extrinsic rotations; the axis pattern alone does not specify that choice.

## Intrinsic ZYZ convention

Starting from aligned frames, turn about current $z$ by $\eta$, current $y$ by $\beta$, and current $z$ by $\gamma$:

$$
R=R_z(\eta)R_y(\beta)R_z(\gamma).
$$

The equivalent fixed-axis sequence is $z$ by $\gamma$, $y$ by $\beta$, then $z$ by $\eta$. With $c_\eta=\cos\eta$, $s_\eta=\sin\eta$, and similarly for the other angles,

$$
R=\begin{bmatrix}
c_\eta c_\beta c_\gamma-s_\eta s_\gamma&-c_\eta c_\beta s_\gamma-s_\eta c_\gamma&c_\eta s_\beta\\
s_\eta c_\beta c_\gamma+c_\eta s_\gamma&-s_\eta c_\beta s_\gamma+c_\eta c_\gamma&s_\eta s_\beta\\
-s_\beta c_\gamma&s_\beta s_\gamma&c_\beta
\end{bmatrix}.
$$

Notice the third column: the first two turns set the final $z$-axis direction; the final turn spins the $x$ and $y$ axes around it.

## Recover the angles

For the branch $0<\beta<\pi$, $\sin\beta$ is positive:

$$
\beta=\operatorname{atan2}\left(\sqrt{r_{13}^2+r_{23}^2},r_{33}\right),\quad
\eta=\operatorname{atan2}(r_{23},r_{13}),\quad
\gamma=\operatorname{atan2}(r_{32},-r_{31}).
$$

The square root recovers $|\sin\beta|$. The chosen branch removes that sign ambiguity. The alternative triplet $(\eta+\pi,-\beta,\gamma+\pi)$ gives the same matrix, modulo complete turns.

### Worked example

Choose $(\eta,\beta,\gamma)=(90^\circ,90^\circ,0^\circ)$:

$$
R=\begin{bmatrix}0&-1&0\\0&0&1\\-1&0&0\end{bmatrix}.
$$

The formulas return $\beta=\operatorname{atan2}(1,0)=90^\circ$, $\eta=\operatorname{atan2}(1,0)=90^\circ$, and $\gamma=\operatorname{atan2}(0,1)=0^\circ$. The alternative $(270^\circ,-90^\circ,180^\circ)$ produces the same orientation.

## Singular cases

When $\sin\beta=0$, the first and last rotation axes align or oppose each other. The separate outer angles cannot be determined:

| Middle angle | What can be recovered | One valid choice |
| --- | --- | --- |
| $\beta=0$ | $\eta+\gamma=\operatorname{atan2}(r_{21},r_{11})$ | Set $\gamma=0$, assign the sum to $\eta$ |
| $\beta=\pi$ | $\eta-\gamma=\operatorname{atan2}(-r_{21},-r_{11})$ | Set $\gamma=0$, assign the difference to $\eta$ |

For example, at $\beta=0$, outer angles $(20^\circ,40^\circ)$ and $(60^\circ,0^\circ)$ both reduce to $R_z(60^\circ)$. These are orientation-coordinate singularities, just as the $\pm90^\circ$ pitch cases are for our roll–pitch–yaw convention, but they occur at different middle angles.

**Checkpoint:** Does “ZYZ” by itself specify the chronological order of fixed-axis operations? No: state intrinsic/extrinsic, which angle belongs to each operation, and the matrix product.

[Previous](03-roll-pitch-yaw.md) · [Section index](README.md) · [Next: Axis–angle](05-axis-angle.md)
