# Actuators and Feedback Devices

The controller needs both a way to produce effort and measurements relevant to its task. Actuator type does not by itself determine whether the full system uses feedback.

## Stepper motors and servo systems

| Property | Stepper drive | Servo system |
| --- | --- | --- |
| Basic idea | Command a sequence of electromagnetic steps or microsteps | Use feedback to regulate position, velocity, or effort |
| Position command | Often specified by pulse count | Reference compared with measured state |
| Speed command | Often specified by pulse frequency | Speed reference tracked through the control loop |
| Feedback | Often open-loop; closed-loop stepper systems also exist | Feedback is part of the definition |
| Limits | Available torque, acceleration, resonance, and missed steps | Available torque, bandwidth, tuning, sensing, and saturation |

For a 1.8° full-step motor, one revolution requires $360/1.8=200$ full steps. At 1000 full-step pulses/s:

$$
\text{speed}=\frac{1000}{200}=5\text{ rev/s}=300\text{ rpm}.
$$

Changing pulse frequency changes commanded speed even without feedback. The motor must still have enough torque to follow the acceleration and load. With 16 microsteps per full step, the same 1000 pulses/s commands $1000/(200\times16)=0.3125$ rev/s, or 18.75 rpm. Finer command increments do not guarantee equally fine physical positioning accuracy. See a manufacturer's explanation of [step commands and closed-loop stepper systems](https://www.orientalmotor.com/stepper-motors/technology/stepper-motor-basics.html).

Compare actual torque-speed curves, thermal limits, gearing, duty cycle, and required tracking performance. Neither “stepper” nor “servo” guarantees lower cost, greater efficiency, or higher accuracy for every application. Holding current can consume power even when an electric motor is stationary.

Pneumatic actuators use compressed gas; hydraulic actuators use pressurized liquid. Both can be combined with position or force feedback. Their valves, pressure supply, compliance, and friction influence control response.

## What each measurement means

| Device | Measurement or inference | Important limitation |
| --- | --- | --- |
| Rotary/linear encoder | Angle or displacement; rate estimated over time | Resolution is not complete tool-position accuracy; incremental systems need a reference |
| Potentiometer | Position inferred from calibrated voltage | Wear, electrical noise, and calibration affect estimates |
| Force/torque sensor | Mechanical load in defined directions | Bias, mounting, gravity, and dynamic loads affect interpretation |
| Camera | Image data used to infer scene geometry | Calibration, visibility, and processing latency matter |
| Proximity sensor | Presence or distance, depending on sensor type | Detection depends on material, range, and geometry |
| Accelerometer and gyroscope | Specific force and angular rate, respectively | Orientation requires estimation; integration drifts, and gravity complicates acceleration interpretation |
| Temperature sensor | Local temperature | Thermal lag and sensor location affect detection of overheating |
| Current sensor | Electrical current | Current-to-torque estimates depend on motor calibration, transmission, and friction |

An ideal 4096-count-per-revolution joint measurement gives $360/4096\approx0.0879^\circ$ per count. State whether the quoted count includes encoder decoding and gearing before converting it to a joint increment.

## Quick reference

A sensor contributes feedback only when its measurement affects a command or decision. See [control layers](01-feedback-and-control-layers.md) for loop boundaries and [tactile sensing](../05-perception-and-autonomous-grasping/03-tactile-and-slip-sensing.md) for contact-specific filtering. Sensor resolution, estimation accuracy, and control bandwidth are distinct properties.

[Previous](04-collaborative-robots.md) · [Section index](README.md) · [Next: Dynamics and feedforward](06-dynamics-and-feedforward.md)
