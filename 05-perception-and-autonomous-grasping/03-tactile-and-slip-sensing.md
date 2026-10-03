# Tactile and Slip Sensing

Vision helps select an approach. Contact sensing helps determine what actually happens when the fingers touch the object.

## Different sensors answer different questions

| Sensor | Measurement | Interpretation limits |
| --- | --- | --- |
| Fingertip force sensor | Contact load at its sensing location | Needs calibration and a defined force direction |
| Force-sensing resistor | Resistance changes associated with applied load | Nonlinearity, hysteresis, and contact geometry affect force estimates |
| Wrist six-axis force/torque sensor | Three forces and three moments at the wrist | Measures a combined wrench, not each finger's force separately |
| Optical slip sensor | Relative surface displacement in its sensing plane | Depends on surface texture, distance, and mounting |

An optical mouse-type tracker can support slip detection in a gripper. This principle has been demonstrated in [optical tracking for prosthetic-hand grip adjustment](https://pmc.ncbi.nlm.nih.gov/articles/PMC10947720/). It measures local motion rather than directly measuring friction coefficient or object weight.

## Position samples to slip velocity

Let $s_k$ be a calibrated relative displacement sample at time step $k$, in meters. One filter is exponential smoothing:

$$
\bar{s}_k=\alpha s_k+(1-\alpha)\bar{s}_{k-1},\qquad 0<\alpha\leq1.
$$

Then estimate velocity using sample period $\Delta t$:

$$
\hat v_k=\frac{\bar{s}_k-\bar{s}_{k-1}}{\Delta t}.
$$

For an illustrative $\alpha=0.03$, previous smoothed displacement 0, and new displacement 0.001 m, the new smoothed value is 0.00003 m. At 1000 Hz, $\Delta t=0.001$ s, so the estimated velocity is 0.03 m/s. This is a filtered transient estimate, not the unfiltered 1 m/s sample-to-sample rate.

Differentiation magnifies noise; low-pass filtering the velocity estimate can help, at the cost of delay. A third-order Butterworth filter with a 45 Hz cutoff at 1000 Hz sampling is one possible experimental choice, not a universal setting. Filter order describes the filter dynamics; cutoff is not a sharp boundary eliminating every higher frequency. Sampling rate, filtering delay, noise, and expected slip speed must be considered together.

An 8200 counts-per-inch sensor setting would nominally correspond to $25.4/8200\approx0.00310$ mm per count. That is nominal resolution, not verified displacement accuracy. Real contact geometry and surface tracking need calibration. Logging at 1000 Hz also does not prove 1000 Hz mechanical control bandwidth.

## Using contact to refine alignment

Small exploratory movements can reveal how contact forces change with tool orientation. For example, compare measured force during bounded left/right or up/down probing, then adjust alignment to reduce a task-defined imbalance. A nearly zero average signal alone does not prove correct alignment: loss of contact, symmetric loading, or sensor bias can produce a similar result. Maintain evidence of contact and check the relevant geometry.

A wrist wrench can guide surface exploration, but gravity, acceleration, and tool offsets contribute to that wrench. Interpret measurements in a declared frame and compensate known loads before attributing every change to the surface.

## Quick reference

Force describes contact loading; slip describes relative movement. Bilateral contact means both gripping sides have contacted the object, not merely that a wrist sensor reports a nonzero resultant. Filtering trades noise reduction for responsiveness.

[Previous](02-visual-servoing.md) · [Section index](README.md) · [Next: Adaptive grasping](04-adaptive-grasping.md)
