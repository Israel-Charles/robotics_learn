# Worked Solutions · Robotics Foundations

Each exercise is repeated below so you can read its reasoning alongside the question. Attempt the [exercises](exercises.md) first.

## 1. Identify components

**Question.** A robot uses a camera to locate a box, wheel motors to approach it, encoders to measure wheel rotation, and a gripper to lift it. Identify two sensors, two kinds of actuators, and the end effector. What software responsibilities are still needed?

**Solution.**

Classify each component by what it does, rather than by whether it moves:

| Component | Category | Reason |
| --- | --- | --- |
| Camera | Sensor | Measures light to form an image of the scene |
| Wheel encoders | Sensors | Measure wheel or shaft rotation |
| Wheel motors | Actuators | Convert supplied energy into wheel rotation |
| Gripper motor or cylinder | Actuator | Produces motion or force to close the fingers |
| Gripper assembly | End effector | Makes task contact with the box |

The gripper includes the contacting mechanism; the actuator is the device driving that mechanism. A gripper's own actuator closes its fingers. In a mobile manipulator, arm or lift actuators raise the held box; gripping and lifting are different actions.

Software must turn camera measurements into a usable box location, plan an approach and grasp, command the motors, use feedback to regulate motion, and verify whether the object was actually acquired. Merely having a camera and motors does not specify how these tasks are coordinated.

## 2. Mechanism and operation

**Question.** Compare an operator-guided arm and an arm repeating a stored path. Does either need a mobile base or AI to be a robotic system? What changes between the operating modes?

**Solution.**

Neither arm needs a mobile base or AI to be a robotic system. An arm attached to a workbench can perform its entire task in the space around that bench.

The difference is who supplies the ongoing motion choices:

| Operation | Source of motion choices | What the controller still does |
| --- | --- | --- |
| Operator-guided | A person moves a joystick or another interface | Converts those commands into actuator behavior and may regulate joint motion with feedback |
| Stored path | A previously taught or programmed sequence | Executes the sequence and may regulate the same joint motion with feedback |

For example, a person can guide a tool around a part once, and the controller can later repeat a recorded path. The arm's links and joints need not change. Its operating mode changes, while feedback control can remain active in both modes.

## 3. Choose the subject

**Question.** Classify each question as primarily kinematics, dynamics, or control: (a) Where is the tool at given joint angles? (b) What torque holds a payload against gravity? (c) How should commands respond when the measured angle lags the desired angle?

**Solution.**

**(a) Kinematics.** The known inputs are joint angles and arm geometry. We seek tool position, so the question is about the geometric relationship between configuration and pose. Mass and motor torque are unnecessary for the ideal calculation.

**(b) Dynamics.** Holding a load requires balancing forces and torques. Even when nothing is accelerating, gravity still creates a load. For a simple horizontal lever with a downward force $F$ applied at perpendicular distance $d$ from its pivot, the torque magnitude is $\tau=Fd$. This illustrates why payload and lever arm matter; a complete arm calculation must also account for its links and other loads.

**(c) Control.** The desired motion is already specified, but the measurement differs from it. A controller computes the tracking error and chooses how to respond. With a desired angle of $30^\circ$ and measured angle of $27^\circ$:

$$
e=\theta_{\mathrm{desired}}-\theta_{\mathrm{measured}}=30^\circ-27^\circ=3^\circ.
$$

That error is information for the controller, not a torque value by itself. The control law and physical limits determine the resulting actuator command.

## 4. Interpret measurements

**Question.** A target coordinate is 50.0 mm. Repeated measurements are 48.9, 49.0, and 49.1 mm. Calculate the mean and signed mean error. Explain why repeatability and accuracy are different here.

**Solution.**

First calculate the average measured position:

$$
\bar{x}=\frac{48.9+49.0+49.1}{3}\text{ mm}
=\frac{147.0}{3}\text{ mm}=49.0\text{ mm}.
$$

Define signed error as measured minus target. The mean error is

$$
\bar{e}=\bar{x}-x_{\mathrm{target}}=49.0-50.0=-1.0\text{ mm}.
$$

The negative sign means the average result falls below the target coordinate. Its error magnitude is 1.0 mm. Inspect individual errors and deviations from the mean:

| Measurement (mm) | Error from 50.0 mm target (mm) | Deviation from 49.0 mm mean (mm) |
| --- | --- | --- |
| 48.9 | −1.1 | −0.1 |
| 49.0 | −1.0 | 0.0 |
| 49.1 | −0.9 | +0.1 |

The full observed spread is $49.1-48.9=0.2$ mm. Results are close to one another, but centered 1.0 mm away from the target. This demonstrates why a system can repeat consistently while having an accuracy problem. The small sample illustrates the distinction; it is not a full repeatability specification.

## 5. Task decomposition

**Question.** Describe two things that must happen between detecting a part and successfully lifting it. Explain why reaching the part is insufficient by itself.

**Solution.**

One possible sequence is:

1. **Choose the grasp.** Convert the detected part location into the robot's frame and select where the fingers should contact it. Seeing the object does not yet specify how to hold it.
2. **Reach the grasp pose.** Find suitable joint angles and a clear approach path. Check that the gripper has room to open and close.
3. **Establish contact.** Close the fingers with suitable force, or activate the relevant gripping mechanism.
4. **Check and lift.** Use available sensing to assess grasp success, then lift while respecting payload and motion limits.

Any two well-explained steps between detection and lifting answer the first part. Reaching the object's location alone is insufficient: the fingers may be misaligned, the gripper may close on empty space, or the grasp may slip under load. Successful manipulation requires both suitable motion and suitable contact.

[Exercises](exercises.md) · [Section index](README.md) · [Next section](../02-manipulators-and-motion/README.md)
