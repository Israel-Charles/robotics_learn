# Collaborative Robots and Physical Interaction

“Industrial” describes an application category; “collaborative” describes how people and robot systems can work together. A collaborative robot can therefore also be an industrial robot.

## Compare the application, not just the arm

| Application pattern | Typical arrangement | What to examine |
| --- | --- | --- |
| Separated operation | Robot operates in a safeguarded space during automatic motion | Access, stopping behavior, tools, and workpieces |
| Collaborative operation | People and the system share a workspace under defined conditions | Human access, possible contact, speed, load, tooling, and protective functions |

A cobot label alone does not establish that every application permits unrestricted contact or operation without guarding. Collaboration can involve monitored stopping, hand guidance, speed/separation monitoring, or power/force limitation, depending on the application. The complete installation—including the end effector and handled object—needs assessment. See the [OSHA technical manual on industrial robot systems](https://www.osha.gov/otm/section-4-safety-hazards/chapter-4) for the application-level distinction.

## Physical human–robot interaction

In physical interaction, forces pass between a person and the robot. A layered controller can use an outer impedance objective to choose compliant behavior and an inner controller to realize it. An inner robust method, such as sliding-mode control, is designed to tolerate specified model uncertainties; its performance still depends on assumptions, sampling, actuator limits, and effects such as chattering.

Consider a tool moving over a curved compliant surface. Its objectives might be to align with the local surface, maintain normal force, and follow a tangential velocity. These objectives use the force/motion separation introduced in the [contact-control lesson](03-force-and-impedance-control.md). If the surface estimate is wrong, an intended tangential movement can push into the surface instead.

## What passivity does and does not establish

At a one-dimensional interaction port, power is $P=Fv$ with a consistent sign convention. Work exchanged over time is the integral of power. A passive system cannot supply unlimited net energy from nothing: energy delivered is bounded by energy previously supplied and initially stored.

For example, a constant 2 N force acting through 0.01 m transfers $W=F\Delta x=0.02$ J. A controller's delay or discretization can change its energy behavior, so passivity must be established for the implemented system and relevant assumptions.

Passivity can support stability reasoning for interconnected systems. It does not, by itself, guarantee comfortable contact, low peak force, or absence of injury. A passive spring can still store substantial energy, and a sharp tool can concentrate force over a small area.

## Checkpoint and quick reference

Does adding a compliant controller make a pointed tool harmless near a person? No. The task, tool geometry, energy, operating limits, and verified protective measures all matter.

- Collaborative and industrial are overlapping descriptions.
- Impedance specifies response to interaction; passivity concerns energy exchange.
- A stability property is not a complete assessment of human contact.

[Previous](03-force-and-impedance-control.md) · [Section index](README.md) · [Next: Actuators and feedback](05-actuators-and-feedback-devices.md)
