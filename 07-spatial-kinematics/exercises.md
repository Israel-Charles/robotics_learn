# Spatial Kinematics Exercises

Use right-handed frames, column vectors, and the conventions in the lessons. Angles marked with $^\circ$ are in degrees. Show the frame or multiplication order before calculating.

1. **Rotation or reflection.** For $R=R_z(90^\circ)$, express $(1,2,3)^T$ in the rotated result and verify its length is unchanged. Explain why $\operatorname{diag}(1,1,-1)$ is not a proper rotation even though it also preserves length.

2. **Order and operator coordinates.** Starting from identity, compare current-$x$ then current-$y$ rotations of $90^\circ$ with fixed-$x$ then fixed-$y$ rotations of $90^\circ$, by applying each result to $(0,0,1)^T$. If ${}^{A}R_B=R_y(90^\circ)$, express an active rotation $Q_A=R_z(\delta)$ in frame $B$.

3. **Roll–pitch–yaw branches.** Extract one roll–pitch–yaw triplet from $R=\begin{bmatrix}0&-1&0\\\sqrt3/2&0&1/2\\-1/2&0&\sqrt3/2\end{bmatrix}$, and give the second branch. Explain why $(20^\circ,90^\circ,50^\circ)$ and $(0^\circ,90^\circ,30^\circ)$ represent the same orientation without implying a mechanical singularity.

4. **ZYZ extraction.** Recover a principal ZYZ triplet from $R=\begin{bmatrix}0&-1&0\\0&0&1\\-1&0&0\end{bmatrix}$. At middle angle $0^\circ$, give two outer-angle pairs that yield $R_z(60^\circ)$. At middle angle $180^\circ$, which combination of outer angles remains identifiable?

5. **Axis–angle limits.** Find a principal axis–angle description and rotation vector for $R=\operatorname{diag}(-1,-1,1)$. Explain why the antisymmetric-entry formula fails here and why adding arbitrary rotation vectors is not a general composition rule.

6. **Quaternion composition.** In scalar-last order, let $q=(0,0,\sqrt2/2,\sqrt2/2)$. Find $q\otimes q$, state its rotation, and find the result of rotating $(1,0,0)^T$ by $q$. Give the halfway SLERP orientation from identity to $q$, and explain whether $-q$ represents a different orientation.

7. **Points, vectors, and inverse transforms.** Let ${}^{A}T_B$ have rotation $R_z(90^\circ)$ and translation $(1,2,3)^T\ \mathrm m$. Transform both a point and a displacement with $B$ coordinates $(0.2,0,0)^T\ \mathrm m$. Find the inverse translation and use the inverse transform to recover the original point.

8. **Local translation in a chain.** Let ${}^{A}T_B$ have rotation $R_z(90^\circ)$ and translation $(1,0,0)^T\ \mathrm m$. Let ${}^{B}T_C$ have identity rotation and translation $(1,0,0)^T\ \mathrm m$. Find ${}^{A}T_C$. Separately, find the translation of $\mathcal R_x(90^\circ)\mathcal T_x(0.2)\mathcal T_z(0.3)\mathcal R_z(45^\circ)$, with distances in metres.

9. **DH and tool offsets.** For the planar arm with $a_1=0.4\ \mathrm m$, $a_2=0.3\ \mathrm m$, $\theta_1=30^\circ$, and $\theta_2=60^\circ$, give its standard DH table and compute frame 2's pose in frame 0. A tool is mounted $0.1\ \mathrm m$ along frame 2's positive $x$ with no relative rotation. Find the TCP position. Which parameter would vary for a prismatic DH joint?

[Section index](README.md) · [Worked solutions](solutions.md)
