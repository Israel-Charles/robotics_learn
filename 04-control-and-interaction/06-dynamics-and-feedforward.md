# Dynamics, Feedforward, and Disturbances

Kinematics relates motion variables. **Dynamics** relates motion to the forces and torques needed to produce it. The same trajectory can require different effort with a different payload.

## Start with one rotating joint

For an illustrative joint with constant rotational inertia $I$, viscous friction coefficient $b$, gravity load $g(q)$, and externally applied disturbance torque $\tau_{\mathrm{ext}}$:

$$
I\ddot q+b\dot q+g(q)=\tau_{\mathrm{cmd}}+\tau_{\mathrm{ext}}.
$$

Here $q$ is angle, $\dot q$ angular velocity, and $\ddot q$ angular acceleration. Each term has torque units. Gravity compensation is needed even at rest if the configuration creates a gravitational load.

**Inverse dynamics** calculates required effort for specified motion using a model. With no external disturbance, $I=0.2$ kg·m², $\ddot q_d=1$ rad/s², $b=0.1$ N·m·s/rad, $\dot q_d=0.5$ rad/s, and gravity load 0.8 N·m:

$$
\tau_{\mathrm{ff}}=0.2(1)+0.1(0.5)+0.8=1.05\text{ N}\cdot\text{m}.
$$

The inertia term supplies acceleration, the friction term overcomes modeled motion resistance, and the gravity term supports the load.

## Feedforward and feedback work together

Feedforward uses the reference and a model to anticipate required effort. Feedback responds to measured tracking error. A simple combination is

$$
\tau_{\mathrm{cmd}}=\tau_{\mathrm{ff}}+K_p(q_d-q)+K_d(\dot q_d-\dot q).
$$

If angle error is 0.02 rad, rate error is 0.1 rad/s, $K_p=10$ N·m/rad, and $K_d=0.5$ N·m·s/rad, the added torque is $10(0.02)+0.5(0.1)=0.25$ N·m. The combined command is 1.30 N·m.

A disturbance such as an unexpected load can create error despite feedforward. Feedback can reduce it, but finite gains, delays, and saturation limit disturbance rejection. A proportional controller may require a nonzero steady error to supply an unmodeled constant torque; feedback does not automatically mean zero error.

## Multiple joints and computed torque

A common rigid-arm model is

$$
M(q)\ddot q+C(q,\dot q)\dot q+g(q)=\tau+\tau_{\mathrm{ext}},
$$

where $M$ is the inertia matrix, $C\dot q$ represents velocity-dependent coupling, and $g$ represents gravity. Friction can be modeled separately. Off-diagonal inertia terms express coupling: accelerating one joint can affect effort at others.

Computed-torque control uses an estimated model with a feedback-adjusted acceleration:

$$
\tau=\hat M(q)\bigl(\ddot q_d+K_v\dot e+K_a e\bigr)
+\hat C(q,\dot q)\dot q+\hat g(q),\qquad e=q_d-q.
$$

Here $K_v$ and $K_a$ have units s⁻¹ and s⁻²; they act inside an acceleration expression, unlike the torque-level gains above. With an exact model, no external disturbance, and no saturation, substitution gives $\ddot e+K_v\dot e+K_a e=0$. Model errors and hardware limits prevent assuming this ideal result automatically. See [Modern Robotics on computed torque](https://modernrobotics.northwestern.edu/nu-gm-book-resource/11-4-motion-control-with-torque-or-force-inputs-part-3-of-3/).

## Quick reference

Inverse dynamics computes effort from motion. Feedforward anticipates modeled loads. Feedback responds to error. Computed torque combines state-dependent model terms with acceleration feedback; it is not purely open-loop replay of a torque sequence.

[Previous](05-actuators-and-feedback-devices.md) · [Section index](README.md) · [Practice](exercises.md)
