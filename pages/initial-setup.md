---
layout: default
title: "Initial Setup"
permalink: /initial-setup/
nav:
- Wiring and Connections: wiring-and-connections
- Install QGroundControl: install-qgroundcontrol
- Loading Firmware: loading-firmware
- Connect QGC to Controller: connect-qgc-to-controller
- Calibration: calibration
- Configuring Parameters: configuring-hardware
---

# {{page.title}}

First-time setup of the autopilot includes downloading and installing the QGroundControl GCS, mounting the controller to the vehicle, connecting it to the tether, power, and motors, and then performing initial configuration and calibration.

## Wiring and Connections

The exact wiring configuration depends on the vehicle configuration and the hardware used. The following is the standard used for all vehicles with six or fewer thrusters. Please see the [frame configurations](/introduction/#supported-frames) for standard thruster numbering.

| PWM Channel | Connection  |
|------------:|:------------|
| Channel 1   | Thruster #1 |
| Channel 2   | Thruster #2 |
| Channel 3   | Thruster #3 |
| Channel 4   | Thruster #4 |
| Channel 5   | Thruster #5 |
| Channel 6   | Thruster #6 |
| Channel 7   | LED Lights  |
| Channel 8   | Camera Tilt Servo |

The hardware also has other input/output ports including I<sup>2</sup>C and serial ports. These are the recommended connections for those ports.

| Port                    | Connection                             |
|------------------------:|:---------------------------------------|
| I<sup>2</sup>C          | Pressure sensor (MS58XX)               |
| Telem1 Serial Port      | Tether (if using serial)               |
| Telem1 Serial Port      | Companion computer (if using Ethernet) |
| Power Port              | Power Module                           |

### Tether Interface Wiring

To be completed.

## Install QGroundControl

We recommend using the most recent daily build of QGroundControl, which can be [downloaded and installed from here](http://qgroundcontrol.org/downloads). Downloads are available for Android, Windows, Mac OS, and Linux.

## Loading Firmware

During the early stage of ArduSub development (now), there are no compiled firmware files available and the firmware must be compiled directly. 

Please see the [Developer section](/developers/) for instructions on how to do so.

## Connect QGC to Controller

The controller can be connected to QGC through several different methods depending on the hardware used.

### Serial Port Connection

If using a serial port, simply connect the port to the computer and open QGC. The controller should automatically connect to QGC and onboard data will be downloaded.

### Ethernet Connection with Companion Computer

If using an Ethernet connection with companion computer, you must [to be completed].

### Ethernet Connection with Linux Autopilot (Navio, BBBmini, etc.)

For Linux based autopilots, the network connection is launched when the ArduSub code is started. For examples, please see the documentation for your respective autopilot.

## Calibration

Once the controller is connected to QGC for the first time, we must calibrate the accelerometers, compass, and joystick.

1. Go to the settings tab in QGC and select the red *Sensors* tab on the left sidebar.
2. Choose your autopilot orientation (none for the BlueROV).
3. Click on *Accelerometers* and follow the instructions.
4. Click on *Compass* and follow the instructions.
5. When completed, the *Sensors* tab will no longer be red.

## Configuring Parameters

A number of parameters should be adjusted at startup for use with ArduSub. The following table shows the currently recommmended parameters to change.

| Parameter         | Value                |
|------------------:|:---------------------|
| ARMING_CHECK      | Disabled             |
| ATC_ACCEL_Y_MAX   | Disabled             |
| BRD_SAFETYENABLE  | Disabled             |
| DISARM_DELAY      | 0                    |
| EK_ALT_NOISE      | 0.1                  |
| GND_PRIMARY       | 2ndBaro              |
| PILOT_VELZ_MAX    | 50 cm/s              |
| PILOT_ACCEL_Z     | 50 cm/s/s            |
| POS_Z_P           | 8.0 (above limit)    |
| RATE_YAW_FILT_HZ  | 30                   |

### Setup Voltage and Current Measurement

On the *Power* tab choose the appropriate setup. If using the standard 3DR Power Module, choose *Analog Voltage and Current*, the appropriate battery capacity, and the *Power Module 90A*.

### Flight Mode Setup

Currently only the *Stabilize* (Manual) and *AltHold* (Learning) modes are used. On the *Flight Modes* tab, set all flight modes to *Stabilize* except for "Flight Mode 6", which should be set to *AltHold*.

### Camera Tilt Setup (if used)

Select the *Camera* tab. The "Gimbal Tilt" settings are used for the camera tilt. Choose *Channel 8* (or whichever channel the servo is plugged into) for "Output channel" and *RC8* for "Input channel". Select *Servo* for the "Type" under "Gimbal Settings" on the right.

We also recommend checking the *Stabilize* box, which will enable auto-stabilization of the camera based on the vehicle pitch angle.

### Lights Setup

The lights feature is currently setup to support lights that use a standard servo PWM signal for control. Until light support is officially added to QGC, the "Gimbal Roll" settings are used to connect the light input to a servo output.

Select *Channel 7* for the "Output channel" and *RC9* for the "Input channel".
