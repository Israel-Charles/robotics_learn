# Standard DH and Forward Kinematics

For a planar two-link arm, adding two displacement vectors is enough to derive forward kinematics. Spatial arms benefit from a repeatable way to assign frames and combine joint motions. Homogeneous matrices provide that bookkeeping; they are not a requirement for every possible kinematic calculation.

## Standard Denavit–Hartenberg convention

DH uses carefully chosen link frames to describe each adjacent transform with four parameters. We use this **standard DH** indexing:

- Joint $i$ rotates about, or slides along, $z_{i-1}$.
- Choose $x_i$ along a common normal between $z_{i-1}$ and $z_i$, directed from the former toward the latter when separated. The origin of frame $i$ lies where that normal meets $z_i$.
- Choose $y_i=z_i\times x_i$ to complete a right-handed frame.

For intersecting axes, the common-normal distance is zero; choose $x_i$ perpendicular to both. Parallel axes permit choices of where the common normal lies along them. Coincident axes permit additional choices. Select frames consistently, record the choices, and use the tool requirements to choose the final axis/frame.

| Parameter | Meaning in this convention | Typical status |
| --- | --- | --- |
| $\theta_i$ | Angle from $x_{i-1}$ to $x_i$ about $z_{i-1}$ | Variable for a revolute joint |
| $d_i$ | Offset along $z_{i-1}$ to the common normal | Variable for a prismatic joint |
| $a_i$ | Common-normal distance along $x_i$ between the two $z$ axes | Fixed geometry |
| $\alpha_i$ | Twist from $z_{i-1}$ to $z_i$ about $x_i$ | Fixed geometry |

Angles follow the right-hand rule. Distances/offsets are signed according to the chosen axes. A joint variable can include a fixed zero offset, for example $\theta_i=q_i+\theta_{i,0}$. For a prismatic joint, $d_i=q_i+d_{i,0}$ and $\theta_i$ is fixed.

The DH parameter $a_i$ is often called a **link length**, but it need not equal the overall length of a physical link housing. For our planar arm it equals the joint-to-joint or joint-to-tip distance. This is why the planar lessons use $a_1,a_2$.

## The adjacent transform

Using $4\times4$ elementary motions,

$$
{}^{i-1}T_i=\mathcal R_z(\theta_i)\mathcal T_z(d_i)\mathcal T_x(a_i)\mathcal R_x(\alpha_i)
=\begin{bmatrix}
c_\theta&-s_\theta c_\alpha&s_\theta s_\alpha&a_i c_\theta\\
s_\theta&c_\theta c_\alpha&-c_\theta s_\alpha&a_i s_\theta\\
0&s_\alpha&c_\alpha&d_i\\
0&0&0&1
\end{bmatrix},
$$

where $c_\theta=\cos\theta_i$, $s_\theta=\sin\theta_i$, and similarly for $\alpha_i$. Modified DH uses different frame assignments and ordering. Do not transfer a parameter table between conventions without rederiving its transforms. For a software example of the two matrix forms, see the [Robotics Toolbox implementation](https://jhavl.github.io/ropy/_modules/ropy/robot/Link.html#Link.A).

## Recover the planar two-link model

Place $z_0$ at the shoulder and $z_1$ at the elbow, both out of the plane. Place $z_2$ at the tip parallel to them, with $x_1$ and $x_2$ along their respective links:

| $i$ | $\theta_i$ | $d_i$ | $a_i$ | $\alpha_i$ |
| --- | --- | --- | --- | --- |
| 1 | $\theta_1$ | $0$ | $a_1$ | $0$ |
| 2 | $\theta_2$ | $0$ | $a_2$ | $0$ |

Multiply ${}^{0}T_2={}^{0}T_1{}^{1}T_2$. Its rotation is $R_z(\theta_1+\theta_2)$ and its position is

$$
\mathbf p=\begin{bmatrix}
a_1\cos\theta_1+a_2\cos(\theta_1+\theta_2)\\
a_1\sin\theta_1+a_2\sin(\theta_1+\theta_2)\\0
\end{bmatrix}.
$$

For $a_1=0.4\ \mathrm m$, $a_2=0.3\ \mathrm m$, $\theta_1=30^\circ$, and $\theta_2=60^\circ$, the position is approximately $(0.3464,0.5000,0)^T\ \mathrm m$ and the orientation is $90^\circ$ about $z$.

## Include the installed base and tool

For an $n$-joint chain,

$$
{}^{W}T_{\mathrm{TCP}}={}^{W}T_0
\left({}^{0}T_1{}^{1}T_2\cdots{}^{n-1}T_n\right)
{}^{n}T_{\mathrm{TCP}}.
$$

The outer transforms describe the base installation and fixed tool mounting. The TCP need not coincide with the last DH-frame origin. Frame labels make the multiplication order checkable, and the same chain structure works when links or tools change. Verify the model at the chosen zero configuration and a simple nonzero configuration before using it for inverse kinematics.

[Previous](07-homogeneous-transformations.md) · [Section index](README.md) · [Practice](exercises.md)
