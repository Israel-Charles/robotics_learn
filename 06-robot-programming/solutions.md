# Worked Solutions · Robot Programming

## 1. Teaching methods

**Question.** An operator guides a robot through selected poses, then runs those poses repeatedly. Identify the teaching and execution methods. Does online programming require the internet or normal production to be running? Why do two stored endpoints not completely define the tool's route?

**Solution.** Physically guiding a suitable robot to record poses is lead-through or hand-guided teaching. Executing the recorded behavior is playback. Online programming means using the actual robot and controller during preparation; it requires neither internet access nor continuing normal production.

Endpoints leave interpolation unspecified. A joint-interpolated motion and a straight TCP motion can share endpoints but take different routes. The program also needs frames, tool configuration, orientation behavior, timing, and limit checks. Selected waypoints do not necessarily capture every intermediate pose of the hand-guided motion.

## 2. Simulation and calibration

**Question.** A program was validated with a workpiece origin at $(0.4,0.2)$ m. The actual origin is $(0.42,0.2)$ m with unchanged orientation. Find the displacement of a workpiece-relative pickup target in the base frame. What must still be checked after updating that frame?

**Solution.** With unchanged orientation, every point fixed in the workpiece frame shifts by the difference between frame origins:

$$
\Delta p=(0.42-0.4,0.2-0.2)=(0.02,0)\text{ m}.
$$

Updating the workpiece frame shifts the target coherently by 20 mm along base $x$. Verify target reachability, intermediate path clearance, joint limits, TCP and payload settings, and relevant physical signals. The original simulation used a different spatial relationship, so its previous clearance result does not automatically carry over.

## 3. Task logic

**Question.** A program closes a gripper, waits 0.5 s, and transfers without checking contact. Explain a possible failure and propose an advance condition plus a failure transition. Does writing this logic in Python make the program inherently offline? Is ROS a programming language?

**Solution.** If the part is absent or misaligned, the fingers can close on empty space. Waiting establishes elapsed time, not a successful grasp. Require an appropriate grasp-confirmation condition before transfer; if it is not met within a timeout, enter a defined recovery state and prevent the normal transfer sequence. Continue monitoring the held object when the task requires it.

Python specifies how the logic is written, not whether it is prepared or tested with the physical robot. Code can be edited offline, simulated, or executed through a connected interface. ROS provides robotics tools, libraries, and communication infrastructure; it is not itself a programming language.

[Exercises](exercises.md) · [Section index](README.md) · [Course index](../README.md)
