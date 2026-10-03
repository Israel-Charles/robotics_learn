# Exercises · Robotics Foundations

Attempt these before reading the [solutions](solutions.md).

1. **Identify components.** A robot uses a camera to locate a box, wheel motors to approach it, encoders to measure wheel rotation, and a gripper to lift it. Identify two sensors, two kinds of actuators, and the end effector. What software responsibilities are still needed?
2. **Mechanism and operation.** Compare an operator-guided arm and an arm repeating a stored path. Does either need a mobile base or AI to be a robotic system? What changes between the operating modes?
3. **Choose the subject.** Classify each question as primarily kinematics, dynamics, or control: (a) Where is the tool at given joint angles? (b) What torque holds a payload against gravity? (c) How should commands respond when the measured angle lags the desired angle?
4. **Interpret measurements.** A target coordinate is 50.0 mm. Repeated measurements are 48.9, 49.0, and 49.1 mm. Calculate the mean and signed mean error. Explain why repeatability and accuracy are different here.
5. **Task decomposition.** Describe two things that must happen between detecting a part and successfully lifting it. Explain why reaching the part is insufficient by itself.

[Section index](README.md)
