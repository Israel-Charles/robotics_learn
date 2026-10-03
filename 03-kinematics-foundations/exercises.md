# Exercises · Kinematics Foundations

Use meters and counterclockwise-positive angles. For the arm problems, assume ideal unlimited joints and no collisions unless otherwise stated.

1. **Unit conversion.** Convert $45^\circ$ and $-90^\circ$ to radians.
2. **Frame transformation.** Frame B is rotated $90^\circ$ relative to A, with B's origin at $(0.5,0.2)$ m in A. A point has B-frame coordinates $(0.1,0.2)$ m. Find its A-frame coordinates, then recover the B-frame coordinates using the inverse mapping.
3. **Forward kinematics.** For $L_1=0.4$ m, $L_2=0.3$ m, $\theta_1=90^\circ$, and $\theta_2=-90^\circ$, find the elbow position, tool position, and tool orientation.
4. **Inverse kinematics.** For $L_1=0.4$ m, $L_2=0.3$ m, and target $(0.3,0.4)$ m, find both elbow branches and their tool orientations. Verify both by forward kinematics.
5. **Unreachable target.** For $L_1=0.4$ m and $L_2=0.3$ m, calculate $c_2$ for target $(0.8,0)$ m. Explain why there is no real IK solution.
6. **Apply limits.** For $L_1=0.4$ m, $L_2=0.3$ m, and target $(0.4,0.3)$ m, suppose joint 1 must lie between $-45^\circ$ and $45^\circ$, and joint 2 between $-120^\circ$ and $120^\circ$. Which branch from the lesson survives? Does that prove a collision-free path exists?
7. **Exceptional geometry.** If $L_1=L_2=0.3$ m, explain how the tool can stay at the base while the shoulder angle changes. What happens to tool orientation?
8. **Mini-lab.** Using $L_1=0.4$ m and $L_2=0.3$ m, adapt the forward-kinematics Python example to evaluate $(0^\circ,0^\circ)$, $(90^\circ,0^\circ)$, $(0^\circ,180^\circ)$, and $(30^\circ,60^\circ)$. Record position, orientation, and distance from the base for each. Explain any tiny values near zero in the numerical output.

9. **Velocity mapping.** For $L_1=0.4$ m, $L_2=0.3$ m, $\theta_1=0$, and $\theta_2=\pi/2$, calculate the position Jacobian. Find tool velocity for joint rates $(0.2,-0.1)$ rad/s, then find joint rates that produce tool velocity $(0,0.04)$ m/s at that configuration.
10. **Singular motion.** For the same positive link lengths, use $\det J=L_1L_2\sin\theta_2$ to identify singular elbow angles. At $\theta_1=\theta_2=0$, can joint motion produce horizontal tool velocity 0.01 m/s? Give two joint-rate pairs producing vertical velocity 0.07 m/s and explain whether a physical joint has lost its freedom.

[Solutions](solutions.md) · [Section index](README.md)
