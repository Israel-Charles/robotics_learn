# Task Logic and Text-Based Programs

A useful robot program specifies what should happen when the expected result does not occur. Commands, measurements, and completion conditions should be distinguishable.

## Language, framework, and controller

Text-based code can be prepared offline or edited while connected to a controller. It is a representation of the program, not a separate synonym for offline programming.

Python and C++ are general-purpose languages. Industrial controllers may use manufacturer-specific languages and motion instructions. A robotics framework supplies communication, device interfaces, and other software infrastructure. For example, [ROS is an ecosystem of tools and libraries](https://github.com/ros2/ros2_documentation/blob/rolling/source/About-ROS.rst), not a programming language or a replacement for every internal motor-control loop.

## Represent the operation as states

| State | Action | Evidence needed to advance |
| --- | --- | --- |
| Ready | Check setup and availability | Part present and destination available |
| Approach | Execute planned approach motion | Motion completes without reported fault |
| Grip | Close or activate the tool | Grasp criteria met before timeout |
| Transfer | Execute the transfer path | Motion complete and grasp maintained |
| Release | Open or deactivate the tool | Release confirmed |
| Recover | Stop normal sequence and handle the failure | Explicit recovery condition or operator intervention |

A controller accepting a command is different from completing it. A fixed delay is different from a sensor confirming contact. A grip-confirmed signal must have a defined meaning, such as adequate contact and object presence; “gripper closed” alone may also mean the fingers closed on empty space.

## Illustrative pseudocode

```text
require validSetup and partPresent and destinationReady
moveTo(pickupApproach)
waitForMotionOrFault()
moveTo(pickupPose)
waitForMotionOrFault()
closeGripper()

if not waitForGraspConfirmation(timeout):
    enterRecovery("grasp not confirmed")
    stopNormalSequence()
else:
    followTransferPathWhileMonitoringGrasp()
    if transferCompletedWithoutFault:
        releaseObject()
        verifyReleaseOrEnterRecovery()
```

This is a logic sketch, not executable robot API code. Faults, timeouts, or loss of grip must prevent the normal sequence from silently continuing. Recovery itself needs task-specific behavior, especially if an object is already held.

## Checkpoint and quick reference

What happens if an object is missing but the program waits 0.5 s after closing and then lifts? It can lift an empty gripper because elapsed time does not establish a grasp. Add a relevant measured condition and a defined failure transition.

Use descriptive state and variable names. Keep frames and units attached to motion data. Test task logic independently from geometry, then validate their interaction.

[Previous](02-offline-programming-and-simulation.md) · [Section index](README.md) · [Practice](exercises.md)
