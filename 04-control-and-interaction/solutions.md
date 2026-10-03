# Worked Solutions · Control and Interaction

## 1. Feedback boundary

**Question.** An arm uses encoder feedback to follow stored joint targets, but never checks whether its gripper acquired an object. Which behavior is closed-loop and which task outcome is not fed back? Would logging camera images alone change that?

**Solution.** Joint motion is closed-loop because measured joint state affects commands. Grasp success is not fed back: a failed pickup does not change the task sequence. Logging images supplies records, but it becomes task feedback only if the images influence a command or decision, such as retrying after a failed grasp. State the loop boundary before applying either label.

## 2. Path and timing

**Question.** A path is $p(s)=(0.2+0.4s,0.1)$ m, with $s=t/2$ for $0\leq t\leq2$ s. At 1 s the measured position is $(0.3,0.1)$ m. Find the scheduled position, desired horizontal speed, distance from the path, and position-tracking error magnitude.

**Solution.** At 1 s, $s=1/2=0.5$, giving

$$
p_d=(0.2+0.4\times0.5,0.1)=(0.4,0.1)\text{ m}.
$$

The desired speed is 0.4 m of horizontal travel divided by 2 s, or 0.2 m/s. The measured point lies on the segment, so its geometric distance from the path is zero. The desired-minus-measured position error is $(0.4-0.3,0.1-0.1)=(0.1,0)$ m, with magnitude $\sqrt{0.1^2+0^2}=0.1$ m. Being on the correct route does not establish correct timing.

## 3. Contact response

**Question.** A gripper uses $v_{\mathrm{close}}=k_F(F_d-F_a)$ with positive velocity meaning closing. Calculate its command for $k_F=0.002$ m/(N·s), $F_d=5$ N, and $F_a=6$ N. Separately, find static displacement under a 4 N external force for virtual stiffness 200 N/m. Which calculation regulates force and which describes impedance?

**Solution.** The force error is $5-6=-1$ N, so

$$
v_{\mathrm{close}}=0.002(-1)=-0.002\text{ m/s}.
$$

The negative command opens the gripper under the stated convention, tending to reduce excessive force. This is force regulation.

For the static impedance calculation, velocity and acceleration vanish. Thus $K_d e=F_{\mathrm{ext}}$ and

$$
e=\frac{4\text{ N}}{200\text{ N/m}}=0.02\text{ m}.
$$

This specifies how much displacement accompanies the external load. It does not prescribe a constant contact force independent of displacement.

## 4. Shared workspace

**Question.** A robot wipes a horizontal surface while a person can approach. Assign force and motion objectives to appropriate directions. Explain why a cobot label and a passive controller do not establish safety for every tool and task.

**Solution.** For a surface whose normal is along $z$, regulate contact force along $z$ and command wiping motion along tangential $x$ and/or $y$. Set a suitable orientation separately and update the task frame if the surface direction changes. Demanding incompatible rigid position and force in the same constrained direction would conflict.

The label describes intended collaborative capabilities, but the full installation includes the tool, workpiece, loads, and possible human contact. Passivity constrains energy generation; it does not impose a harmless peak force or remove sharp edges. For example, stored spring energy can be released during contact even by a passive mechanism. The actual application and protective functions need assessment.

[Exercises](exercises.md) · [Section index](README.md) · [Next section](../05-perception-and-autonomous-grasping/README.md)
