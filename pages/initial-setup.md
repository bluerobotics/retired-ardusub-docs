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

The exact wiring configuration depends on the vehicle configuration and the hardware used. The following is the standard use for all vehicles with six or fewer thrusters. Please see the [frame configurations](#) for standard thruster numbering.

| PWM Channel | Connection  |
|:-----------:|:------------|
|      1      | Thruster #1 |
|      2      | Thruster #2 |
|      3      | Thruster #3 |
|      4      | Thruster #4 |
|      5      | Thruster #5 |
|      6      | Thruster #6 |
|      7      | LED Lights  |
|      8      | Camera Tilt Servo |

| Port                    | Connection                             |
|:-----------------------:|:---------------------------------------|
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

Please refer to the ArduPilot documentation for basic instructions on building the code.

- [Mac Instructions](http://dev.ardupilot.com/wiki/building-px4-with-make-on-mac/)
- [Linux Instructions](http://dev.ardupilot.com/wiki/building-px4-for-linux-with-make/)
- [Windows Instructions](http://dev.ardupilot.com/wiki/building-px4-with-make/)

To compile the ArduSub branch, first `cd ArduSub` to enter the directory and then use a command with the following format:

``` bash
make [board type]-[frame type]-[upload (optional)]
```

For example,

``` bash
make px4-v2-vectored-upload
```

The available board types can be seen by entering `make` with no arguments. Below are the available frame types.

| Command | Function |
| --- | --- |
| `bluerov`      | Compile for BlueROV thruster configuration |
| `vectored`     | Compile for vectored w/ side-by-side vertical thruster configuration |
| `vectored6DOF` | Compile for vectored w/ corner vertical thruster configuration |

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