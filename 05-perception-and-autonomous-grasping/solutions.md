# Worked Solutions · Perception and Autonomous Grasping

## 1. Stereo geometry

**Question.** With focal length 600 px and baseline 0.08 m, find depth for disparities of 40 and 20 px. Which point is farther away? Explain why a matching error matters and why a depth estimate is not yet a grasp command.

**Solution.** Use the rectified stereo relationship $Z=fb/d$:

$$
Z_{40}=\frac{600(0.08)}{40}=1.2\text{ m},\qquad
Z_{20}=\frac{600(0.08)}{20}=2.4\text{ m}.
$$

The smaller-disparity point is farther away. A wrong correspondence changes disparity and therefore changes estimated depth, potentially by a large amount. Depth must still be combined with contact geometry, gripper opening, coordinate transforms, inverse kinematics, and collision checks. Seeing a reachable surface does not prove the object can be held securely.

## 2. Visual feedback

**Question.** A point is observed at $(360,220)$ px and desired at $(320,240)$ px. Find current-minus-desired image error. Classify a controller using this error, one using reconstructed target pose, and one combining image centering with reconstructed orientation. Can the pixel error be sent directly as a displacement in meters?

**Solution.** Subtract coordinate by coordinate:

$$
e=(360-320,220-240)=(40,-20)\text{ px}.
$$

The image-error controller is IBVS, the reconstructed-pose controller is PBVS, and the mixed controller is hybrid visual servoing. The pixel coordinates express observations on the image, not physical translation distances. A valid conversion depends on camera geometry, depth, and the controlled motion. One point alone also provides too few independent measurements to determine all six spatial pose freedoms in general.

## 3. Filtered slip

**Question.** A displacement filter uses $\alpha=0.03$, previous smoothed displacement zero, new sample 0.001 m, and sample period 0.001 s. Calculate the smoothed displacement and finite-difference velocity. Explain one benefit and one cost of further low-pass filtering.

**Solution.** Substitute into the smoothing equation:

$$
\bar{s}_k=0.03(0.001)+0.97(0)=0.00003\text{ m}.
$$

Then calculate rate of change:

$$
\hat v_k=\frac{0.00003-0}{0.001}=0.03\text{ m/s}.
$$

Further filtering can attenuate noise amplified by differentiation, but it delays the response to genuine slip. A controller that reacts to stale estimates may permit more movement before adjusting force. Neither high sample rate nor fine nominal sensor resolution eliminates this tradeoff.

## 4. Grip adaptation

**Question.** Two equal opposing contacts hold a static 2 N weight with friction coefficient 0.4. Find minimum ideal normal force per finger and total normal force. Then calculate one force-target update from 4 N with gain 100 N/m, slip speed 0.01 m/s, threshold 0.002 m/s, and interval 0.02 s, assuming clipping does not activate. Explain why this calculation does not establish a safe force for every object.

**Solution.** Both contacts together supply at most $2\mu N$ friction. Therefore

$$
N_{\min}=\frac{W}{2\mu}=\frac{2}{0.8}=2.5\text{ N per finger},\qquad
F_{g,\min}=2N_{\min}=5\text{ N}.
$$

For the illustrative update, slip above threshold is $0.01-0.002=0.008$ m/s. The target increment is

$$
\Delta F_d=100(0.008)(0.02)=0.016\text{ N},\qquad
F_{d,k+1}=4+0.016=4.016\text{ N}.
$$

Using the lesson's total-normal-force convention, this updated target is still below the ideal static requirement of 5 N. A controller using per-finger force would instead compare its target with the 2.5 N per-finger bound. Keep the sensor and target conventions consistent. Unknown friction, asymmetry, dynamics, and a crushing limit require additional information. A force update is not proof that slip will stop or that the object will tolerate the force.

## 5. Demonstration frames

**Question.** An unrotated bowl frame is at $(0.4,0.2)$ m and the demonstrated tool point is $(0.45,0.2)$ m. Find the relative point and its new base-frame position when the bowl moves to $(0.6,0.3)$ m without rotation. Find the interpolated scalar position halfway between 0.2 m and 0.4 m. Explain why resampling and fitting a GMM do not automatically make the resulting motion feasible.

**Solution.** With no frame rotation, subtract the bowl origin:

$$
p^O=(0.45-0.4,0.2-0.2)=(0.05,0)\text{ m}.
$$

Add the new origin to preserve that relationship:

$$
p^B_{\mathrm{new}}=(0.6,0.3)+(0.05,0)=(0.65,0.3)\text{ m}.
$$

At interpolation fraction $\lambda=0.5$,

$$
p=(1-0.5)(0.2)+0.5(0.4)=0.3\text{ m}.
$$

Resampling aligns phase samples, not necessarily contact events. A GMM describes demonstrated variation but does not independently enforce joint limits, obstacle clearance, or contact-force requirements. New frame positions can place a statistically plausible motion outside the robot's workspace. Validate generated motion and execute it with appropriate feedback.

[Exercises](exercises.md) · [Section index](README.md) · [Course index](../README.md)
