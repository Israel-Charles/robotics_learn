# Visual Servoing

Visual servoing uses camera-derived measurements repeatedly to adjust robot motion. Detecting a target once and executing a stored movement without further visual updates is a different feedback arrangement.

## What error does the controller reduce?

| Approach | Error representation | Information needed |
| --- | --- | --- |
| Position-based visual servoing (PBVS) | Difference between estimated current and desired spatial pose | Pose estimation and consistent camera/robot frames |
| Image-based visual servoing (IBVS) | Difference between current and desired image features | Feature tracking and a model relating camera motion to feature motion |
| Hybrid or 2.5D visual servoing | A combination of image features and reconstructed geometric quantities | Tracking plus the geometry needed for the selected reconstructed quantities |

PBVS uses reconstructed geometry, while IBVS defines the controlled error in image measurements. Both depend on estimation and modeling, and both can have visibility or convergence limitations. See [Chaumette and Hutchinson's tutorial](https://web.mit.edu/amcp/OldFiles/drg/Chaumette_Part_I.pdf) for their mathematical formulation.

## An image error is not a motor command

Suppose a tracked image point is at $(360,220)$ px and its desired location is $(320,240)$ px. Defining error as current minus desired gives

$$
e_{\mathrm{image}}=\begin{bmatrix}360-320\\220-240\end{bmatrix}
=\begin{bmatrix}40\\-20\end{bmatrix}\text{ px}.
$$

This identifies an image displacement, not a 40 mm robot movement. Depth, focal length, camera mounting, and robot configuration affect how physical motion changes those pixels. One point also cannot generally constrain all six camera-motion freedoms. A visual controller needs an appropriate set of features and a valid feature-to-motion relationship.

In PBVS, stereo observations can instead estimate the target's spatial pose. The desired gripper pose includes a grasp offset relative to that target and a camera-to-base transform. Re-estimate and update as motion proceeds; object pose alone is not a tool command.

## Homography-based hybrid control

For matched points on a plane in two views, a homography relates homogeneous image coordinates through $\tilde p'\sim H\tilde p$. The symbol $\sim$ means equality up to nonzero scale. With camera calibration and appropriate geometric assumptions, decomposing this mapping can recover rotation and translation relative to plane distance. Absolute metric scale needs additional information, and multiple decompositions may require disambiguation.

A hybrid controller can combine image centering with reconstructed rotation and depth-related quantities. “2.5D” names a mixture of representations, not half a physical degree of freedom. [Malis, Chaumette, and Boudet](https://www.cs.jhu.edu/~hager/Public/teaching/CS600.641/Malis2-1-2DTRA99.pdf) develop this approach.

Two views may come from two cameras or a moving camera; successive views require sufficient scene consistency and known or estimated motion geometry. “Pseudo-stereo” does not itself guarantee metric depth. A feature tracker, including a fern-based classifier trained on image patches, establishes correspondences; it is not the complete controller. Direct use of pixel-location errors is an image-based component even when embedded in a hybrid scheme.

## Checkpoint and quick reference

Why might visual tracking fail near contact? The gripper may hide features, the camera may reach its focus limit, or reflections may change. This motivates complementary contact sensing, not a claim that vision is always slow or unusable.

- PBVS: regulate reconstructed pose.
- IBVS: regulate image features.
- Hybrid VS: combine chosen image and geometric errors.
- Keep feature visibility, calibration, and confidence in the motion decision.

[Previous](01-depth-and-grasp-candidates.md) · [Section index](README.md) · [Next: Tactile and slip sensing](03-tactile-and-slip-sensing.md)
