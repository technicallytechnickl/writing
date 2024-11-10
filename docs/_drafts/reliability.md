---
title: Reliability
layout: post
---

Reliability is defined as the probability of a system performing a given task over a given time period. It is therefore impossible to define the reliability of a system without understanding what those specific tasks are. More specifically, it is impossible to have a highly reliable and highly complex system if every given functionality is included in the reliability calculation. An example could be a modern airliner. No airliner has every function working at all times.  A screen is out on a seat somewhere, a coffee pot doesn't work, a door squeaks. However, the key requirements of an airliner is to keep the humans on board safe and to ideally get them from point A to B.  If we look at the reliability of those tasks, all of those minor failures don't matter at all.  Even an engine could fail and the primary goals could be satisfied. As Capt. Sully demonstrated, even both engines could fail and the primary requirement still be met. That capability is only possible because engineers understand that the primary requirement is safety.  Therefore the aircraft is designed with as many layers of reliability in place as possible with regard to safety. 

 It is impossible to build a complex system to meet a complex set of needs without a detailed understanding of the key requirements of the system.  

Often, when systems are designed to be highly reliable, the cost of deploying the system skyrockets. The costs involved can increase in a non-linear manner as conservatism is built into the design in multiple places.  One example would be purchasing hardened IT equipment that has extended operational temperature ranges, but then having a cooling system to keep the temperature below 60F, and further requiring N+1 redundancy on the cooling equipment.  In this case the requirements end up being redundant and more expensive than necessary. 

Reliability of complex systems can not be addressed by design at a single point.  A complex system consists of vast array of components working harmony to achieve the system requirements.  A SCADA system I developed included the following domains:
- Custom software - multiple languages
- Off the shelf software - FOSS configured and standard
- Off the shelf firmware - Computer BIOS, networked devices and sensors
- Site Configuration - Documentation usable by the control programs of how the site is physically configured
- Databases - monitoring, customer data, billing data
- Networking - multiple brands of switches, fiber, copper, wireless
- SAAS products
- Consumer grade electronics - computers, power distribution units, switches
- Industrial grade electronics - high power relays and power meters, variable frequency drives
- Third party monitoring systems
- Contractual requirements
- An operations team
- An engineering team
- Third party data sources - critical data for real time operations
- Environmental controls - Fans, VFDs

Ensuring the reliability of such a system should address failures across each of these domains.  Reliability must also be ensured as the system and requirements change over time. 


## Design with Parallel Components
A key to reliability in a complex system is *fault tolerance*.  Fault tolerance is the property of a system that a single fault in the system doesn't result in further faults or a total loss of functionality.  This implies that components don't directly rely on each other to perform their functions. 


## What is reliability?
At a top level, reliability is a measure of how often a system does its job in a given time period.  

This concept sounds simple but can quickly get complicated when complex systems are involved.  Even assigning a reliability value to a system implies that the system is observable and predictable enough to do so. Some systems include humans in the loop, which makes reliability much more difficult to achieve and compute. The operating environment can be another complication to computing and achieving reliability. 


In a complex system, not only does the system have a reliability, but so do the physical and software components in the system. 

The key to a reliable system lies in understanding the reliability of the components and building an architecture that can allow component failures without a system failure. Keeping the reliability of individual components conceptually separated from the reliability of the system allows a more robust and affordable architecture to be created. 

When architecting a system, the critical functionalities must be kept in mind, and the components required to provide those functionalities identified. For example, consider a system with a sensor, compute unit, actuator, and display.  The critical requirement is to sense an intruder and actuate the alarm.  A secondary requirement is to display historical detections to a user. That would imply the sensor, compute unit, and actuator are critical components, while the display is not.  

This example leads us to another important concept in reliability, isolation. The above example makes the assumption that the display is isolated from the rest of the system, meaning that the failure of the display will not affect the other components. The more isolated components of a system can be kept, the easier it is to design, analyze, and improve the system. Too many interdependencies can create chaos, and a chaotic system quickly becomes impossible to predict.


### Failure Rates
A key concept to understand in describing reliability is *mean time between failures* or MTBF. MTBF represents the expected time between failures of a system in normal operations.  For instance, a rack server may have an MTBF of 50,000 hours. That means the server is expected to operate almost six years before failing.  However, MTBF is a statistical measure.  That means the server could last two years, or it could last eight years. Those two values are probably low in likelihood, but that really depends on the shape of the distribution of failures for that device.  



Detailed information on failure rates is rarely available for consumer level goods, but some assumptions can be made.

## Planning for Failure

### Burn In

### Graceful Degradation
Another concept to understand in reliability is *graceful degradation*.  Graceful degradation is the concept of the system retaining some functionality even with component failures.  An example from my radar design days is the phased array radar.  In the passive type of this radar, there is a single generator of the signal power that is distributed to a passive antenna.  If that generator fails, the radar has zero functionality.  In the active type of this radar, there are hundreds or thousands of individual elements that generate their own signals.  If one of these elements fail, the beam of the radar broadens slightly and the total power output may drop proportionately. The active phased array radar demonstrates graceful degradation in this case. 

### Redundancy