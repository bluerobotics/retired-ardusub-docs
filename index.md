---
layout: default
title: "Home"
permalink: /
---

# {{ page.title }}

**Firmware for Remote-Operated and Autonomous Capabilities in Underwater Vehicles**

The *ArduSub* project is a fully-featured, open-source controller for remotely operated underwater vehicles (ROVs) and autonomous underwater vehicles (AUVs). Based on the popular *ArduCopter* code, the *ArduSub* code has extensive capabilities out of the box including feedback stability control, depth and heading hold, and autonomous position control if provided with position feedback.

*ArduSub* is designed to be safe, feature-rich, open-ended, and easy to use even for novice users.

## ArduSub in Use

<div class="row">
	<div class="col-md-6">
		<iframe width="400" height="225" src="https://www.youtube.com/embed/BV91zgzEFHs" frameborder="0" allowfullscreen></iframe>
	</div>
	<div class="col-md-6">
		<iframe width="400" height="225" src="https://www.youtube.com/embed/qVMpD-v-dfY" frameborder="0" allowfullscreen></iframe>
	</div>
</div>

## System Components

- A PixHawk or other DroneCode-compatible autopilot loaded with the latest version of the [ArduSub firmware](#).
- [QGroundControl software](#) for setup, configuration, and operation of the vehicle.
- A [suitable ROV or AUV](http://bluerobotics.com) for use with the software
- Many other useful additions: depth sensors, tether communications, cameras, and other sensors and actuators

## ROV/AUV Types

### ROVs

- *ArduSub* currently supports two frame configurations:
	- **BlueROV 6DOF Frame:** Maneuvers with unique 6 degree-of-freedom control
	- **Vectored w/ Side-by-Side Vertical Thrusters:** Provides excellent smooth control and stability 
	- **Vectored w/ Corner Vertical Thrusters:** Provides excellent smooth control, stability, and 6-DOF control
- In the future, other frame types will be supported, such as:
	- **3 and 4 thrusters** arranged with two thrusters for forward/turn and one or two for vertical

### AUVs

- *ArduSub* has not yet been tested with any AUVs but support will be added in the future

## More Info

- Continue to the [Introduction](/introduction/) section of this page.
- Visit [DIYDrones.com](http://diydrones.com), a large community of enthusiasts largely clustered around the ArduPilot family of autopilots.
- Use the [BlueRobotics Forums](http://bluerobotics.com/forums/) to ask support questions and advice.
- Join the [Gitter developer chat room](https://gitter.im/bluerobotics/ardusub) to get quick support and contribute to development.
