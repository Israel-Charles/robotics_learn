# Rotation Order and Frame Changes

“Rotate about $x$, then about $y$” is incomplete until we say whether those axes stay fixed or move with the body.

## Compose coordinate maps

If ${}^{A}R_B$ maps $B$ coordinates into $A$, and ${}^{B}R_C$ maps $C$ into $B$, then

$$
{}^{A}R_C={}^{A}R_B\,{}^{B}R_C.
$$

The adjacent frame labels match. Applied to a column vector, the rightmost matrix acts first: $C\rightarrow B\rightarrow A$. This is a chain of coordinate conversions, independent of any story about physically turning a body.

## Fixed axes and current axes

Let $R$ describe the body's current orientation relative to a fixed frame. A new rotation $Q$ updates it differently depending on where the rotation axis is expressed:

| Axis used for the new rotation | Update | Common name |
| --- | --- | --- |
| Fixed/world-frame axis | $R_{\text{new}}=QR$ | Extrinsic rotation |
| Current/body-frame axis | $R_{\text{new}}=RQ$ | Intrinsic rotation |

Postmultiplication uses the body's current axes; premultiplication uses the fixed axes. These rules follow from the coordinate-map convention, rather than from the axis letters alone. See the [Modern Robotics explanation of rotation composition](https://modernrobotics.northwestern.edu/nu-gm-book-resource/3-2-1-rotation-matrices-part-2-of-2/).

### Worked example: order changes the result

Start aligned with the fixed frame, so $R=I$, and perform two $90^\circ$ rotations:

- About **current $x$**, then **current $y$**: $R=R_x(90^\circ)R_y(90^\circ)$.
- About **fixed $x$**, then **fixed $y$**: $R=R_y(90^\circ)R_x(90^\circ)$.

The body's original $z$ direction, $\mathbf e_z=(0,0,1)^T$, finishes at $(1,0,0)^T$ in the first case and $(0,-1,0)^T$ in the second. In general, $R_xR_y\ne R_yR_x$.

An intrinsic sequence has an equivalent extrinsic sequence with **reversed chronological order** and the same corresponding angles: current $x$ then current $y$ equals fixed $y$ then fixed $x$.

### Mixed-axis sequence

Starting at $I$, rotate about current $x$ by $u$, current $z$ by $v$, fixed $z$ by $w$, current $y$ by $b$, then fixed $x$ by $c$:

$$
R=R_x(c)R_z(w)R_x(u)R_z(v)R_y(b).
$$

Build the product one update at a time. A chronological list cannot simply be copied into a left-to-right matrix product when fixed and current axes are mixed.

## Express the same rotation operator in another frame

Suppose $Q_A$ actively rotates vectors and is expressed in frame $A$. With $S={}^{A}R_B$, the same physical operator in $B$ is

$$
\boxed{Q_B=S^{-1}Q_AS=S^TQ_AS.}
$$

Read from right to left: convert $B$ coordinates to $A$, apply $Q_A$, then convert back to $B$. This **similarity transformation** changes the coordinates of the operator; it does not add another physical rotation.

For example, if $S=R_y(90^\circ)$, $A$'s positive $z$ points along $B$'s negative $x$. Thus an active $R_z(\delta)$ in $A$ is represented by $R_x(-\delta)$ in $B$.

**Checkpoint:** A body has orientation $R$ and turns about its own $z$ by $20^\circ$. The update is $RR_z(20^\circ)$.

[Previous](01-rotation-matrices.md) · [Section index](README.md) · [Next: Roll, pitch, and yaw](03-roll-pitch-yaw.md)
