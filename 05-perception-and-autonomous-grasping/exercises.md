# Exercises · Perception and Autonomous Grasping

1. **Stereo geometry.** With focal length 600 px and baseline 0.08 m, find depth for disparities of 40 and 20 px. Which point is farther away? Explain why a matching error matters and why a depth estimate is not yet a grasp command.
2. **Visual feedback.** A point is observed at $(360,220)$ px and desired at $(320,240)$ px. Find current-minus-desired image error. Classify a controller using this error, one using reconstructed target pose, and one combining image centering with reconstructed orientation. Can the pixel error be sent directly as a displacement in meters?
3. **Filtered slip.** A displacement filter uses $\alpha=0.03$, previous smoothed displacement zero, new sample 0.001 m, and sample period 0.001 s. Calculate the smoothed displacement and finite-difference velocity. Explain one benefit and one cost of further low-pass filtering.
4. **Grip adaptation.** Two equal opposing contacts hold a static 2 N weight with friction coefficient 0.4. Find minimum ideal normal force per finger and total normal force. Then calculate one force-target update from 4 N with gain 100 N/m, slip speed 0.01 m/s, threshold 0.002 m/s, and interval 0.02 s, assuming clipping does not activate. Explain why this calculation does not establish a safe force for every object.
5. **Demonstration frames.** An unrotated bowl frame is at $(0.4,0.2)$ m and the demonstrated tool point is $(0.45,0.2)$ m. Find the relative point and its new base-frame position when the bowl moves to $(0.6,0.3)$ m without rotation. Find the interpolated scalar position halfway between 0.2 m and 0.4 m. Explain why resampling and fitting a GMM do not automatically make the resulting motion feasible.

[Solutions](solutions.md) · [Section index](README.md)
