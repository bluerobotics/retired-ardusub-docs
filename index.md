---
layout: default
title: "Home"
permalink: /
---

# {{ page.title }}

**Firmware for Remote-Operated and Autonomous Capabilities in Underwater Vehicles**

The *ArduSub* project is a fully-featured, open-source controller for remotely operated underwater vehicles (ROVs) and autonomous underwater vehicles (AUVs). Based on the popular *ArduCopter* code, the *ArduSub* code has extensive capabilities out of the box including feedback stability control, depth and heading hold, and autonomous position control if provided with position feedback.

*ArduSub* is designed to be safe, feature-rich, open-ended, and easy to use even for novice users.

## System Components

- A PixHawk or other DroneCode-compatible autopilot loaded with the latest version of the [ArduSub firmware](#).
- [QGroundControl software](#) for setup, configuration, and operation of the vehicle.
- A [suitable ROV or AUV](http://bluerobotics.com) for use with the software
- Many other useful additions: depth sensors, tether communications, cameras, and other sensors and actuators

## ROV/AUV Types

### ROVs

- *ArduSub* currently supports two frame configurations:
	- **Vectored Frame** giving excellent smooth control and stability 
	- **BlueROV 6DOF Frame** for maneuvering in unique 6 degree-of-freedom control
- In the future, other frame types will be supported, such as:
	- **3 and 4 thrusters** arranged with two thrusters for forward/turn and one or two for vertical

### AUVs

- *ArduSub* has not yet been tested with any AUVs but support will be added in the future

## More Info

- Continue to the [Introduction](/introduction/) section of this page.
- Visit DIYDrones.com, a large community of enthusiasts largely clustered around the ArduPilot family of autopilots.
- Use the [BlueRobotics Forums](http://bluerobotics.com/forums/) to ask support questions and advice.
- Join the [Gitter developer chat room](https://gitter.im/bluerobotics/ardusub) to get quick support and contribute to development.
- Read or join the *ardusub email* list once you’re ready to get involved with the development of the software platform.
