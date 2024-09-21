---
title: Reliability is an Onion
layout: post
---

Reliability is an often overlooked aspect of system design and performance.  When reliability is considered, it is often assumed to just be a result, not a target to design for.  In other cases, reliability is designed in at a single layer, typically redundancy.  This has the net effect of a less reliable system, and a higher cost per "unit" of reliability. Designing for reliability in layers has a positive feedback effect resulting in higher reliability levels at lower overall cost in development. This post will discuss one way of approaching layers of reliability in a system. 

Reliability is an onion as the layers build upon each other create a whole that is greater than any individual layer.  The order of the layers are also important as you can strip them off from the outside in and still effectively have a smaller onion.  This allows tailoring of the approach or building and adding as possible. The layers addressed here are:

0. The Core: Requirements
1. Design, Implementation, Verification, and Validation
2. Organizational Processes
3. Conservative design
4. Redundancy
5. Organizational Responsiveness and Reliability
6. Observability and Predictability
7. Graceful degradation
8. Fail-safes
9. Lifetime Verification and Validation Program

By implementing each layer in the development of a complex system, maximum reliability can be achieved with a minimum of cost and development time. 

## The Core - Requirements
The core of building a reliable system is proper understanding, prioritization, and documentation of the requirements of the system. 

It is impossible to build a successful complex system without understanding all of the requirements of the system.  The designers of a system must understand how the system should respond in each situation, planned and unplanned.  They must understand the boundaries of a system and what each interface involves. 

The requirements documents of a complex system may involve millions of individual requirements.  Complexity is the killer of reliability and even the predictability of reliability.  Therefore, reliability begins to mean nothing in the face of so many requirements and so much complexity.  Attempting to design for perfection in all dimensions simultaneously will push the design project past schedule and budget constraints and end up with a fragile system that fails at critical tasks.

In order for a designer to move forward, a simpler set of key requirements must be prioritized.  This simplicity can allow the designer to focus efforts and resources towards the key requirements of a system.  A design team always has limited time available, therefore it makes sense to budget more of that time to key requirements.  Reliability toward key requirements can also be increased through design decisions whereby the system fails at a lesser requirement in order to ensure success at the higher priority requirement. Prioritization allows a designer to move from the impossible task of making a complex system completely reliable to making a simpler subset of that system extremely reliable. 

The specification of a system can be thought of like code meant to be compiled by designers and makers and resulting in the desired system.  Fully specifying a complex system can require thousands or even millions of individual requirements spread across multiple documents and levels of scope of the system.  Requirements generally should be broken down into individual lines where each line is atomic, complete, understandable, verifiable, and justified (traceable to a root). This documentation of requirements forms the foundation of the system that will be designed and built, and therefore must be approached as a critical phase of system development. If the requirements are not correct, complete, or used as the foundation for design decisions, then the resultant system will not pass validation and will not be fit for purpose.

## Design, Implementation, Verification, and Validation
Design, in this context, is the process of making decisions to create a system that addresses a set of requirements. Will the system be analog or digital? Will the system use grid power or generators?  Design is performed from the highest to lowest levels of the system, and in many cases never really ends while the system is operational.  Implementation is the process of creating the system that has been designed.  Writing code, purchasing components, plugging in cables, etc.  Implementation can sound simple, but becomes complex very quickly as systems grow or cross functional boundaries between software, hardware, and process. The design  and implementation of the system sets the maximum achievable reliability of the system and the most likely cost of the system. When a system is being designed, the choices made determine how many layers of reliability will be utilized and how they will be implemented.  The design of the system determines where conservative design, redundancy, operational procedures, etc will be used to achieve the goals of the system.  The implementation determines how close to ideal the system actually is.  Are the cables tight and routed properly or is the OS of the proper version and configured properly. The way to ensure both design and implementation have occurred correctly is through verification and validation. 

Verification and validation are often confusing to people, or even completely ignored. In the creation of reliable systems though, verification and validation are critical.  Verification is the more straight forward to understand of the two processes. Verification ensures that the system as designed and implemented meets the stated requirements. Examples of questions answered by verification include:
- Do specific inputs create specific outputs?  
- Can the system operate under all stated operational environments?  
- Is the system maintainable, and will it achieve it's reliability goals? 

Verification is applied from the lowest level of implementation up to the highest level of integration. Verification should be performed any time changes are made in the system.  Verification can be achieved in several ways including test, analysis, inspection, and demonstration.  Each method has costs and benefits and should be applied when appropriate. 

Where verification ensures that components of the system meet requirements, validation is more concerned that the developed system interacts with the external world in the manner desired.  Often validation is thought of as acceptance of the system by the customer. This is correct, but should be applied within the system and development team as well.  The team responsible for integrating the control system should validate that the hardware and software they receive from other teams performs as required for the rest of the control system.  Then at the next level, the system integration team should validate that all of the major subsystems are performing as desired. In this way validation occurs many times instead of just at final system delivery.

Utilizing an iterative and layered approach to design, implementation, verification, and validation ensures that the system is designed to meet the requirements, is actually built as designed, and that the requirements are appropriate for the actual need.  These are the ultimate measures of reliability and thus are near the core.

## Organizational Processes
At this point in the onion metaphor, the organization itself must be considered. All systems are developed by some sort of organization, and the system tends to reflect the organization that developed it. Organizational processes are not the most exciting layer in the reliability onion, but they are critical in the development of reliable systems.  

The development and deployment of complex systems does not happen all at once. Systems are incrementally and cyclically built and deployed over months and years.  Many complex systems never cease to be developed and deployed.  Over this time period requirements and environments can change, individuals are promoted, leave, and join the organization. No single person knows everything about the system. Only the organization as a whole can contain and maintain the knowledge of the system. Therefore organizational processes are critical to ensure that the development of the system does not drift from the goals it is meant to achieve. Consistency must be maintained across the entire development program. The requirements must remain consistent with the need, the design consistent with the requirements, and the implementation consistent with the design.  

The organizational processes must handle many cases of change in order to maintain this consistency.  They must handle changes in end user needs, or even a complete change in end user.  The processes must handle changes in requirements and drive those changes through the entire system. The process should maintain knowledge such that new team members can be on boarded effectively and understand their context in the program. The processes even have to handle subtle cases such as when someone has a *good idea* that would negatively impact some other piece of the system.  In that case the process should serve to identify the issue and prevent the feature from being implemented.  

A good set of organizational processes are like a reliable system.  There are multiple layers of processes to catch issues in multiple places and ensure that the system is developed appropriately. Organizational processes must be tuned to the program and the team size, but they should never be overlooked in development of a complex system.

## Conservative design
All components in a complex system were designed to operate in specific environments or at specific operating points.  An off the shelf PC may be designed to operate from 0-30C and 10-90% (non-condensing) humidity levels. A ventilation fan is designed to operate at a specific voltage and power level, and to have preventative maintenance performed at specific intervals.  A trade can be made between performance and reliability by selecting the operating point of each component of the system. Selecting for reliability involves ensuring that each of these ratings are de-rated such that the system is even less to have a failure.  For example, performing the preventative maintenance on mechanical equipment at 90% of the rated interval or replacing IT equipment at 90% of their rated lifetime.  Each of these design choices has a real cost in money, performance, or both which may be significant.  Therefore, conservative design should be reserved for critical areas or areas where other layers don't provide sufficient coverage.  The "Jesus Nut" on a helicopter is a good example.  Redundancy can't be applied at this location, but the nut is a single point of catastrophic failure of the entire helicopter.  Therefore it's design is extra-conservative. Extra mass is intentionally spent on the nut to ensure that it does not fail in any operating environment.

Conservative design is an early place in the design to build in reliability.  These choices must be well documented though, as a typical failure mode is future designers or makers seeing "free" performance in moving an operational point, but not understanding the reliability impact changing it will have on the system. 

## Redundancy
Another basic approach to increasing reliability is simple redundancy. Redundancy is different than conservative design as redundancy simply adds another of a critical component.  Though this approach can be expensive, it is also often technically "easy". Adding a third air conditioning unit or paying for an additional fiber run are straight forward compared to some of the other approaches to increased reliability.  Redundancy can also be applied to other layers.  Redundant fail-safes or organizational structures are certainly options to consider. Redundancy falls in the middle of the layers due to the combination of simplicity and cost involved.  

## Organizational Responsiveness and Reliability
The vast majority of complex systems interact with humans at some level of their operation.  Most systems even have teams of humans who exist to maintain and operate the system. Therefore, part of the system design should include consideration for the organizations that will interact with the system.  Those organizations essentially become another component of the system, and their reliability and responsiveness add into the overall system reliability and responsiveness.  If the operators of the system are unreliable, it is unreasonable to expect the system itself to be reliable.  If the maintenance team is unresponsive, then expecting failures in the system to be addressed in a timely manner is unrealistic.  Therefore, designing organizational responsiveness and reliability should be treated with the same importance as any other component of the system. 

The keys to a responsive and reliable organization are communication, documentation, and training.  In order for any organization to operate well, the members must know what their job is.  Training sets the initial stage and provides any critical skills necessary for the job.  However, no one can keep all necessary knowledge in their head at all times.  Therefore documentation of the system and procedures is critical.  The documentation must be sufficient for the operators or maintainers to handle any situations that arise. This layer is also where system maintenance is implemented.  The organization must perform the maintenance required to keep the system operating in the desired reliability range. Training and documentation must cover maintenance required to ensure the system remains operational, and to detect issues before they cause failures.

The third characteristic of responsive and reliable organizations is effective communications.  Information must pass between individuals and organizations effectively. The effectiveness of communications includes the speed of communication and the completeness of the information relayed.  Training and internal systems must be set up such that critical information is identified and passed to the applicable part of the organization quickly.  The information must also be complete enough for the receiving organization to take appropriate action. This is much like the requirements for submitting bug reports. 

## Observability and Predictability
Observability is the capability of the system operators to measure what is happening in the system. The better a system can be measured, the better it's performance can be predicted. If a system is predictable, then undesired states can be prevented or at least mitigated.  Therefore, building a system that is both observable and predictable allows a responsive organization to increase the reliability of the system. 

Observability should be built into systems at as many levels as practical. The closer the observation is to the source of a potential failure mode the better. Examples may be number of reboots, exceptions caught, network latency, temperatures, noise levels, or even scheduled measurements like thicknesses or fracture analysis.  Effective observations and complete documentation not only allow direct detection of issues, but can allow analysts to develop predictive models. Predictive models are the force multiplier of this level.  Development of such models can take time and effort, but being able to predict failures allows optimization of maintenance routines and early action on potential failures. They can remove a whole category of failures if implemented correctly.

## Graceful degradation
Graceful degradation is a design philosophy that focuses on maintaining performance against the most critical requirements as portions of the system fail. The intent is that the system loses capability incrementally, but does not suddenly completely fail. A physical metaphor would be a structural  member made of ductile steel versus a typical graphite composite. The performance of the composite member may be higher, but when it fails there is no remaining performance. The steel member may proportionally lose dimensional accuracy as the load is increased, but the load will not be suddenly dropped. A design that incorporates graceful degradation allows a system to maintain reliability to the most critical requirements even in the most severe circumstances.

A subtlety built into graceful degradation is that the system tends not to fail quickly.  This gives time to respond to failures and repair any issues. This is another force multiplier that builds on having high observability and a responsive organization to create the highest reliability systems possible. 

## Fail Safes
The last line of reliability built into the system itself are the fail safes. When everything else has failed, the system should be designed such that the most critical requirements are still met. These are typically safety requirements and may involve protecting human life, but fail safes can be implemented at any level in the system and can prevent a cascade of small failures from becoming a critical failure.

Fail safes are not only triggered when a failure has occurred.  They can also be triggered when the system has degraded to a critical level, observability has failed, or the organization has failed to act. The key is for the fail safe to be triggered while the necessary amount of time and control is still available. Failsafe systems must be the most reliable individual components of the system and thus need to be very simple, very reliable, and absolute. An example would be the break wires on the Apollo Launch Escape System (LES).  If two of the three wires that ran the length of the rocket were severed, the LES would activate and jettison the crew from the rest of the rocket. The assumption being that if two cables were severed, something really bad probably happened. No crew input or exceptions existed in this system. It is a simple physical if-then mechanism to save the life of the crew. In this case most of the mission would be considered a failure but the highest priority requirement would still be met, which was to keep the astronauts safe. 

## Lifetime Verification and Validation Program
With all of the other layers in place, the final layer is implementing a program or set of processes to verify the other layers.  Fail safes really need to be tested in to ensure they work in all cases.  The system should be pushed to extremes to ensure there are no undetected failure modes. The operational organization should have a chance to ensure their processes are correct and capable of recovering from failures. All of this should be done over the life of the system, especially as requirements, design, or implementation change. 

The lifetime verification and validation program should ensure that the system continues to behave as expected throughout its lifetime and that it is still delivering the required value to the end user.

By approaching reliability in multiple layers, a system can be designed to optimize reliability with a minimal impact on performance and cost.  Multiple approaches to reliability can constructively interact and create a more reliable system than would be achievable with a single approach. 














