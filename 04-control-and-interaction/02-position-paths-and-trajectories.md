# Position, Paths, and Trajectories

A motion request must specify whether location, route, or timing matters.

| Objective | Desired behavior | Example |
| --- | --- | --- |
| Setpoint regulation | Reach and hold a fixed value | Hold a joint at 30° |
| Path following | Stay near a geometric curve; exact arrival time is not prescribed by the path | Trace a seam while allowing progress to vary |
| Trajectory tracking | Follow values prescribed as functions of time | Reach successive points at specified times |

## A path becomes a trajectory when timing is added

Consider a straight planar path, in meters:

$$
p(s)=\begin{bmatrix}0.2+0.4s\\0.1\end{bmatrix},\qquad 0\leq s\leq1.
$$

The dimensionless parameter $s$ describes progress. The path starts at $(0.2,0.1)$ m and ends at $(0.6,0.1)$ m. Choosing $s(t)=t/2$ for $0\leq t\leq2$ s adds timing. At $t=1$ s, the desired point is $(0.4,0.1)$ m, and the desired horizontal speed is $0.4/2=0.2$ m/s. Abrupt starts and stops in this simple timing law require smoothing for acceleration-limited motion.

Suppose the measured position at 1 s is $(0.3,0.1)$ m. It lies exactly on the path, but it is 0.1 m behind the trajectory's scheduled position. Small path error does not imply small tracking error.

## Joint-space and task-space commands

A joint-space reference specifies $q_d(t)$; a task-space reference specifies a tool position or pose. Inverse kinematics can supply joint configurations for task-space points, but independently choosing a solution at each point can switch elbow branches abruptly. A continuous motion needs consistent feasible solutions, timing, and joint-limit checks.

Position and orientation also need different error definitions. Subtracting two position vectors in the same frame is meaningful. Spatial orientation needs an appropriate rotation-error representation.

## Checkpoint and quick reference

If a robot follows a painted line perfectly but pauses for an obstacle, can it still satisfy a time-scheduled trajectory? It may satisfy the geometric path while failing the original schedule.

- Setpoint: one desired state.
- Path: where to move.
- Trajectory: where to be as time advances.
- Timing does not solve collision avoidance or inverse-kinematics continuity by itself.

[Previous](01-feedback-and-control-layers.md) · [Section index](README.md) · [Next: Contact control](03-force-and-impedance-control.md)
