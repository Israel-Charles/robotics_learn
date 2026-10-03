# Exercises · Control and Interaction

1. **Feedback boundary.** An arm uses encoder feedback to follow stored joint targets, but never checks whether its gripper acquired an object. Which behavior is closed-loop and which task outcome is not fed back? Would logging camera images alone change that?
2. **Path and timing.** A path is $p(s)=(0.2+0.4s,0.1)$ m, with $s=t/2$ for $0\leq t\leq2$ s. At 1 s the measured position is $(0.3,0.1)$ m. Find the scheduled position, desired horizontal speed, distance from the path, and position-tracking error magnitude.
3. **Contact response.** A gripper uses $v_{\mathrm{close}}=k_F(F_d-F_a)$ with positive velocity meaning closing. Calculate its command for $k_F=0.002$ m/(N·s), $F_d=5$ N, and $F_a=6$ N. Separately, find static displacement under a 4 N external force for virtual stiffness 200 N/m. Which calculation regulates force and which describes impedance?
4. **Shared workspace.** A robot wipes a horizontal surface while a person can approach. Assign force and motion objectives to appropriate directions. Explain why a cobot label and a passive controller do not establish safety for every tool and task.

5. **Actuator and sensor increments.** A motor has 1.8° full steps and receives 1000 pulses/s. Find commanded rpm in full-step mode and with 16 microsteps per full step. Find angular increment for a joint measurement with 4096 decoded counts per revolution. Explain why neither command increment nor encoder increment is a complete accuracy specification.
6. **Predicted and corrective effort.** A scalar joint model has $I=0.2$ kg·m², $b=0.1$ N·m·s/rad, desired acceleration 1 rad/s², desired speed 0.5 rad/s, and modeled gravity load 0.8 N·m. Find inverse-dynamics feedforward torque. Add feedback with position error 0.02 rad, speed error 0.1 rad/s, $K_p=10$ N·m/rad, and $K_d=0.5$ N·m·s/rad. Explain the role of feedback when the actual payload differs from the model.

[Solutions](solutions.md) · [Section index](README.md)
