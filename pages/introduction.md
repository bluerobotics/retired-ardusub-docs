---
layout: default
title: "Introducing ArduSub"
permalink: /introduction/
nav:
- Overview: overview
- Key Features: key-features
- What You'll Need: what-youll-need
- Supported Frames: supported-frames
- Sensors and Actuators: sensors-and-actuators
- Applications: applications
---

# {{page.title}}

ArduSub is an advanced open-source ROV/AUV control system.

## Overview

ArduSub is a complete open-source controller solution for subsea vehicles, offering both remotely operated control (via a number of intelligent dive modes) and execution of fully autonomous missions.

As part of the [DroneCode Software Platform](https://www.dronecode.org/dronecode-software-platform) it works seamlessly with Ground Control Station software that can monitor vehicle telemetry and perform powerful mission planning activities. It also benefits from other parts of the DroneCode platform, including simulators, log analysis tools, and higher level APIs for vehicle management and control.

ArduSub is on the cutting edge of marine robotics and intended for those people who want to try advanced technology, cutting edge software, and new capabilities. It can be used on many different types of subsea vehicles including several configurations of ROVs.

## Key Features

- **Feedback control and stability:** Based on a multicopter autopilot system, the ArduSub controller has accurate feedback control to actively maintain orientation.
- **Depth hold:** Using pressure-based depth sensors, the ArduSub controller can maintain depth within a few centimeters.
- **Heading hold:** By default, the ArduSub automatically maintains its heading when not commanded to turn.
- **Camera Tilt:** Camera tilt control with servo or gimbal motors through the joystick or gamepad controller.
- **Light Control:** Control of subsea lighting through the joystick or gamepad controller.
- **No Programming Required:** The ArduSub controller works for a variety of ROV configurations without the need for any custom programming. Most parameters can be changed easily through the ground control station.

## What You'll Need

There are numerous potential combinations of hardware and vehicles compatible with the ArduSub controller. Here's a short summary list:

- [Supported ROV](#supported-frames) with thrusters and speed controllers
- Autopilot controller like the 3DR PixHawk
- Tether for communication via serial or Ethernet
- Laptop computer with QGroundControl installed
- USB gamepad or joystick controller ([example](http://www.amazon.com/Logitech-940-000110-Gamepad-F310/dp/B003VAHYQY))
- Pressure sensor for depth measurement ([example](https://www.bluerobotics.com/store/electronics/bar30-sensor-r1/))

### ROV

ArduSub is compatible with many different ROV frames. [Please see here](#supported-frames) for a list of actively supported frames.

### Hardware Controller

With [DroneCode](http://dronecode.org) compatibility, the ArduSub controller is usable with many different hardware options including:

- **PixHawk** from 3DRobotics
- **PixRacer*** from AUAV
- **Navio+/Navio2** from Emlid
- **Erle Brain, PXFmini*** from Erle Robotics
- **BBBmini** shield for BeagleBone Black

*These options have 8 or less PWM outputs and may not support all ArduSub frame types

### Tether and Tether Interfaces

ArduSub is compatible with both serial and Ethernet based communication interfaces. The hardware autopilot used must support the option that you choose. The Pixhawk only supported a serial connection but can be connect to Ethernet through a companion computer. Other autopilots support Ethernet natively.

There are several available tether interface boards that work well with ArduSub:

* To be completed.

### Topside and Ground Control Station

The ArduSub software is designed primarily to interface through QGroundControl (QGC), an open-source, cross-platform user interface for drones of all types. The interface connects to the ArduSub controller through the tether and displays vehicle status information and allows parameters and settings to be updated.

Most importantly, QGC interfaces with the joystick or gamepad controller used to command the vehicle. It is compatible with most USB joysticks. There are several recommended joysticks:

- **Xbox 360 / Xbox One Controller** with wireless USB connection
- **Logitech 310** (wired) and **Logitech 710** (wireless) gamepads

If using an Ethernet-based tether option and computer-based autopilot, then streaming video can be displayed directly in QGC.

## Supported Frames

ArduSub includes a high-level motor library that can configure motors in any configuration. This library is used to implement a number of supported frame configurations. All configurations are shown from **top-down view**. Currently supported are:

<div class="row">
	<div class="col-md-4">
		<img src="/images/bluerov-frame.png" class="img-responsive img-center" style="max-height:250px;">
		<p class="text-center"><strong>BlueROV Configuration</strong> with 6-DOF thruster positioning. (Frame: <code>bluerov</code>)</p>
	</div>
	<div class="col-md-4">
		<img src="/images/vectored-frame.png" class="img-responsive img-center" style="max-height:250px;">
		<p class="text-center"><strong>Vectored ROV</strong> with side-by-side vertical thrusters. (Frame: <code>vectored</code>)</p>
	</div>
	<div class="col-md-4">
		<img src="/images/vectored6dof-frame.png" class="img-responsive img-center" style="max-height:250px;">
		<p class="text-center"><strong>Vectored ROV w/ Four Vertical Thrusters</strong>, an 8-thruster configuration with 6-DOF control and heavy-lifting capacity. (Frame: <code>vectored6dof</code>)</p>
	</div>	
</div>

<div class="row">
	<div class="col-md-4">
		<img src="/images/simplerov-3.png" class="img-responsive img-center" style="max-height:250px;">
		<p class="text-center"><strong>ROV</strong> with a single vertical thruster. (Frame: <code>simplerov</code>)</p>
	</div>
	<div class="col-md-4">
		<img src="/images/simplerov-4.png" class="img-responsive img-center" style="max-height:250px;">
		<p class="text-center"><strong>ROV</strong> with side-by-side vertical thrusters. (Frame: <code>simplerov</code>)</p>
	</div>
</div>

[Please see here](/developers/#making-a-custom-configuration) if you would like to add your own configuration.

## Sensors and Actuators

In addition to the standard onboard sensors (IMU, compass), the ArduSub controller supports a number of external sensors including:

- Pressure/depth sensors for measurement and auto depth-hold ([example](https://www.bluerobotics.com/store/electronics/bar30-sensor-r1/))
- GPS for position at the surface (does not work underwater)

In the future the ArduSub controller will be able to interface with more sensors such as depth sounders, scanning sonars, temperature sensors, and conductivity sensors.

The controller can command dimmable lights and can be configured to control standard servos as well for additional functionality.

## Applications

ArduSub provides the functionality needed for a wide variety of applications from simple observation-class ROVs to sophisticated research-class ROVs. Here's a short list of applications that ArduSub-powered ROVs can be used for:

- Observation and exploration
- Wreck discovery and documenting
- Photography and videography
- Boat and equipment inspection
- Biological sampling and surveying
- Underwater retrieval
- Academic and research projects
- ROV and AUV competitions