# Exercises · Control and Interaction

1. **Feedback boundary.** An arm uses encoder feedback to follow stored joint targets, but never checks whether its gripper acquired an object. Which behavior is closed-loop and which task outcome is not fed back? Would logging camera images alone change that?
2. **Path and timing.** A path is $p(s)=(0.2+0.4s,0.1)$ m, with $s=t/2$ for $0\leq t\leq2$ s. At 1 s the measured position is $(0.3,0.1)$ m. Find the scheduled position, desired horizontal speed, distance from the path, and position-tracking error magnitude.
3. **Contact response.** A gripper uses $v_{\mathrm{close}}=k_F(F_d-F_a)$ with positive velocity meaning closing. Calculate its command for $k_F=0.002$ m/(N·s), $F_d=5$ N, and $F_a=6$ N. Separately, find static displacement under a 4 N external force for virtual stiffness 200 N/m. Which calculation regulates force and which describes impedance?
4. **Shared workspace.** A robot wipes a horizontal surface while a person can approach. Assign force and motion objectives to appropriate directions. Explain why a cobot label and a passive controller do not establish safety for every tool and task.

[Solutions](solutions.md) · [Section index](README.md)
