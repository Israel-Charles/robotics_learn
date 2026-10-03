# Robots, Manipulators, and Autonomy

## A mechanism within a system

A **manipulator** is a mechanism of connected links and joints used to position or move a tool or object. Its working end may carry an **end effector**, such as a gripper, welding torch, suction cup, or inspection sensor.

A complete robotic system combines the mechanism with the hardware and software needed to perform its task. Depending on the application, that may include actuators, sensors, motor drives, a controller, power equipment, and external tools.

The words overlap in everyday use: a powered industrial manipulator with its controller is commonly called a robot arm. The useful distinction is between discussing the mechanism and discussing the integrated system.

| Question | Manipulator as a mechanism | Complete robotic system |
| --- | --- | --- |
| What is being described? | Links, joints, and tool geometry | Hardware and software operating together |
| What is a typical analysis? | Joint motion and tool reach | Sensing, planning, execution, and task success |
| Must it move around the room? | No | No |
| Must it use AI? | No | No |
| Can it be remotely operated? | Yes, when equipped for actuation | Yes |

### Wheels move the robot; a manipulator positions a tool

A wheeled inspection robot can drive through a building and take pictures without having an arm or gripper. Its wheels form its **locomotion system**: their usual job is to move the robot's base relative to the ground. A **manipulator** positions a tool or handles an object relative to its mounting base. Having moving parts alone does not make a mechanism a manipulator.

| Mechanism | Typical job | Usual description |
| --- | --- | --- |
| Driven wheels beneath a robot | Move the robot through its environment | Locomotion system |
| Arm carrying an inspection camera | Position and aim a sensor relative to the arm's base | Manipulator |
| Arm carrying a gripper | Reach for and handle an object | Manipulator with an end effector |

The distinction is based on function. A specialized roller mechanism that turns a workpiece can participate in manipulation, but the driving wheels on an ordinary inspection robot are not normally called its manipulator.

A **mobile manipulator** combines a mobile base with an arm: the wheels bring the system near a shelf, and the arm reaches for an item. A humanoid similarly combines locomotion mechanisms with arms that can manipulate objects.

## Autonomy describes operation

Autonomy concerns what the system can decide and carry out without ongoing human input. It is not determined simply by having an arm, wheels, or a human-like shape.

| Operating mode | Human role | System role |
| --- | --- | --- |
| Teleoperation | Supplies ongoing movement commands | Executes commands, often with local stabilization |
| Programmed automation | Defines a sequence or taught path | Repeats that behavior under expected conditions |
| Supervised autonomy | Sets goals and handles exceptions | Carries out portions of the task independently |
| Greater task autonomy | Specifies a higher-level objective | Interprets observations and chooses actions within its operating limits |

These categories can coexist in one machine. A remotely operated vehicle may automatically stabilize its heading while the operator chooses where to go. A robot may navigate independently but require help when an aisle is blocked.

Always ask: **autonomous for which task, in which environment, and with what human involvement?**

## Example: three ways to use an arm

Consider the same six-joint arm:

1. An operator uses a joystick to guide its tool.
2. A controller repeats a stored transfer path between two fixtures.
3. A camera estimates the pose of a part, and software selects a grasp and generates a new path.

The mechanical arrangement can remain the same while the sensing and decision-making capabilities change. Joint count alone tells you neither how autonomous the arm is nor how well it performs its task.

## Checkpoint

A stationary arm automatically welds parts along a taught path. Is it excluded from being a robot because it cannot drive around or recognize arbitrary objects?

No. Mobility and general object recognition are not requirements for every robotic system.

## Quick reference

- **Manipulator:** the mechanism used to position or manipulate.
- **End effector:** the tool attached at the working end.
- **Mobile manipulator:** a manipulator mounted on a mobile platform.
- **Autonomy:** a task-dependent ability to act without ongoing human direction.

[Previous](01-what-is-robotics.md) · [Section index](README.md) · [Next: From a task to a working system](03-from-task-to-system.md)
