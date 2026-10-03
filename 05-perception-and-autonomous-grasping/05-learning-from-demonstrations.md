# Learning from Demonstrations

A demonstrated motion contains both task relationships and details specific to one setup. Repeating its coordinates in the robot base frame may fail when an object moves.

## Record motion relative to meaningful frames

Consider a feeding task with frames attached to a bowl, a mouth target, and the robot base. Near the bowl, tool motion may need to maintain a particular relationship to the bowl. Near the destination, the mouth frame becomes important. Known frame poses are assumed here; detecting that an image contains a bowl does not by itself estimate its full pose.

**Kinesthetic teaching** records motion while a person guides a robot in an appropriate teaching mode. Recorded variables may include tool pose, joint configuration, time, and interaction measurements. The task representation should identify which measurements are needed and in which frames they are expressed.

Using the coordinate convention from [Coordinate frames](../03-kinematics-foundations/01-coordinate-frames.md), express a recorded base-frame point relative to an object frame O:

$$
p^O=({}^B R_O)^T(p^B-t^B_O).
$$

For an unrotated bowl frame at $(0.4,0.2)$ m and a tool point at $(0.45,0.2)$ m, the bowl-relative point is $(0.05,0)$ m. If the bowl moves to $(0.6,0.3)$ m without rotation, preserving that relative position gives tool point $(0.65,0.3)$ m. Copying the old base coordinates would miss that relationship.

## Align demonstrations in time

Two demonstrations may contain different numbers of samples. Define normalized phase $s\in[0,1]$ and resample each trajectory at common phase values. Linear interpolation between position samples $p_a,p_b$ is

$$
p(s)=(1-\lambda)p_a+\lambda p_b,\qquad
\lambda=\frac{s-s_a}{s_b-s_a}.
$$

Halfway between positions 0.2 m and 0.4 m, $\lambda=0.5$ gives 0.3 m. Equal sample counts do not ensure that meaningful events such as grasp contact occur at matching phases; event alignment may also be necessary. Rotation data require an appropriate orientation interpolation method. Phase alignment also does not choose safe execution speed.

## What a Gaussian mixture model contributes

A **Gaussian mixture model (GMM)** represents a distribution using several weighted Gaussian components. Each component has a mean describing a typical value, a covariance describing spread and correlations, and a mixture weight. For demonstrations, variables might include phase and tool coordinates. The model can describe several local movement patterns rather than one straight average path.

In a task-parameterized formulation, observations are represented in several task frames and transformed using the current frame poses. This can preserve relationships as objects move. See [Calinon's task-parameterized robot-learning framework](https://www.idiap.ch/~scalinon/papers/Calinon-ISRR2015.pdf).

Low variation across demonstrations can suggest a constraint, but it can also reflect too few or overly similar examples. A learned distribution does not establish causal importance or guarantee collision avoidance. An ordinary GMM fit to base-frame points is not automatically aware of bowl or mouth frames.

## From reproduction to evaluation

Generate candidate motion for a new frame arrangement, then check reachability, tool orientation, continuity, collisions, and contact objectives. Evaluate on configurations not used in teaching. In an assistive task, human movement and comfort impose additional constraints beyond reproducing the demonstrated path.

## Quick reference

Task frames encode relationships; time alignment makes samples comparable; a statistical model describes variation. Generalization still depends on the demonstrated range, frame estimates, robot constraints, and execution feedback.

[Previous](04-adaptive-grasping.md) · [Section index](README.md) · [Practice](exercises.md)
