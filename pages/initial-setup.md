---
layout: default
title: "Initial Setup"
permalink: /initial-setup/
nav:
- Wiring and Connections: wiring-and-connections
- Install QGroundControl: install-qgroundcontrol
- Loading Firmware: loading-firmware-on-pixhawk
- Setup Raspberry Pi: set-raspberry-pi
- Connect QGC to Controller: connect-qgc-to-controller
- Calibration: calibration
- Configuring Joystick/Gamepad: configuring-joystickgamepad
- Configuring Parameters: configuring-parameters
- Configuring Motor Directions: configuring-motor-directions
---

# {{page.title}}

First-time setup of the autopilot includes downloading and installing the QGroundControl GCS, mounting the controller to the vehicle, connecting it to the tether, power, and motors, and then performing initial configuration and calibration.

## Wiring and Connections

The exact wiring configuration depends on the vehicle configuration and the hardware used. The following are the standard channel assignments. Please see the [frame configurations](/introduction/#supported-frames) for standard thruster numbering.

| PWM Channel | Connection  |
|------------:|:------------|
| Channel 1   | Thruster #1 |
| Channel 2   | Thruster #2 |
| Channel 3   | Thruster #3 |
| Channel 4   | Thruster #4 (if used) |
| Channel 5   | Thruster #5 (if used) |
| Channel 6   | Thruster #6 (if used) |
| Channel 7   | Thruster #7 (if used) |
| Channel 8   | Thruster #8 (if used) |
| User Configurable | LED Lights  |
| User Configurable | Camera Tilt Servo |

The hardware also has other input/output ports including I<sup>2</sup>C and serial ports. These are the recommended connections for those ports.

| Port                    | Connection                             |
|------------------------:|:---------------------------------------|
| I<sup>2</sup>C          | Pressure sensor (MS58XX)               |
| Telem1 Serial Port      | Tether (if using serial)               |
| USB Serial Port         | Companion computer (if used)           |
| Power Port              | Power Module                           |

### Serial Tether Interface Wiring

This section describes the overall wiring setup when using a tether interface with analog video and serial port communication such as the Blue Robotics Fathom-S Tether Interface.

[To be completed]

### Ethernet Tether Interface Wiring

[To be completed]

## Install QGroundControl

We recommend using the most recent daily build of QGroundControl, which can be [downloaded and installed from here](https://donlakeflyer.gitbooks.io/qgroundcontrol-user-guide/content/download_and_install.html). Downloads are available for Android, Windows, Mac OS, and Linux.

## Loading Firmware on Pixhawk

Compiled firmware is now available and can be downloaded from [firmware.ardusub.com](http://firmware.ardusub.com). Firmware is only available for the following hardware right now:

* Pixhawk (px-v2)

Please see the [Developer section](/developers/) for instructions on how to compile from source.

### Loading Through QGroundControl

Install the most recent daily build of [QGroundControl](https://donlakeflyer.gitbooks.io/qgroundcontrol-user-guide/content/download_and_install.html) and navigate to the *Firmware* tab of the settings page.

<img src="/images/qgc/firmware-1.png" class="img-responsive img-center" />

Plug in the Pixhawk to the computer's USB port. Once detected, QGroundControl will show a firmware selection box on the right. Choose "ArduPilot Flight Stack" and then check the "Advanced Settings" checkbox. From the dropdown box that appears, choose "Custom firmware file...".

<img src="/images/qgc/firmware-2.png" class="img-responsive img-center" />

Press "OK" at the top right and you will be prompted to select the firmware file (which will probably be named "ArduSub-v2.px4"). Make sure you [download the most recent firmware](http://firmware.ardusub.com) and choose it here.

The firmware will upload the Pixhawk and you'll see the following printout and success message.

<img src="/images/qgc/firmware-3.png" class="img-responsive img-center" />

## Setup Raspberry Pi

If using the *Advanced Electronics Package*, a Raspberry Pi computer is used as a *companion computer* with the Pixhawk. The computer handles video streaming and relaying communications to the surface through an Ethernet connection.

For information on how to set up the Raspberry Pi for use with ArduSub, see the [Raspberry Pi Setup Page](/raspi-setup/).

## Connect QGC to Controller

The controller can be connected to QGC through several different methods depending on the hardware used.

### Serial Port Connection

If using a serial port, simply connect the port to the computer and open QGC. The controller should automatically connect to QGC and onboard data will be downloaded.

### Ethernet Connection with Companion Computer

If an Ethernet connection is used, then a *companion computer* must be used to relay communications between the Pixhawk autopilot and the surface computer. The Pixhawk is connected to the *companion computer* via USB.

Please see the [Raspberry Pi Setup](/raspi-setup/) page for more details on setting up the *companion computer*.

### Ethernet Connection with Linux Autopilot (Navio, BBBmini, etc.)

For Linux based autopilots, the network connection is launched when the ArduSub code is started. For examples, please see the documentation for your respective autopilot.

## Calibration

Once the controller is connected to QGC for the first time, we must calibrate the accelerometers, compass, and joystick.

1. Go to the settings tab in QGC and select the red *Sensors* tab on the left sidebar.
2. Choose your autopilot orientation:
	- `None` for level orientation (such as the BlueROV1)
	- `Roll90` for the BlueROV2
3. Click on *Accelerometers* and follow the instructions.
4. Click on *Compass* and follow the instructions.
5. When completed, the *Sensors* tab will no longer be red.

## Configuring Joystick/Gamepad

*ArduSub* provides a number of parameters to map controller buttons to various functions. This setup is required as there are no defaults configured.

We recommend the button assignments shown in the image below:

<img src="/images/controller.png" class="img-responsive img-center" />

Each button can be assigned to one primary function and one alternate "shift" function. If the "shift" functions are used, then a "shift" button must be assigned. This works like the shift key on your keyboard, altering the functionality of other buttons while pressed.

In the parameters, you will find a number of parameters named `BTN1_FUNCTION` (normal function) and `BTN1_SFUNCTION` (shift function) for each button. You can find the button numbers on the "joystick" tab in QGroundControl.

Note, if using a Logitech gamepad, pressing the "mode" button causes the left joystick and the button pad to switch places. Make sure the light next to "mode" is *not* illuminated.

The following is a list of functions that can be assigned to buttons:

* None
* Shift
* ArmToggle
* Arm
* Disarm
* ModeToggle
* EnterFlightMode1
* EnterFlightMode2
* EnterFlightMode3
* EnterFlightMode4
* EnterFlightMode5
* EnterFlightMode6
* CameraMountTilttoCenter
* CameraMountTiltUp
* CameraMountTiltDown
* CameraShutterTrigger
* CameraSourceToggle
* Lights1CycleBrightness
* Lights1IncreaseBrightness
* Lights1DecreaseBrightness
* Lights2CycleBrightness
* Lights2IncreaseBrightness
* Lights2DecreaseBrightness
* GainToggle
* GainIncrease
* GainDecrease
* TrimRollRight
* TrimRollLeft
* TrimPitchUp
* TrimPitchDown
* InputHoldToggle

## Configuring Parameters

A number of parameters should be adjusted at startup for use with ArduSub. The following table shows the currently recommended parameters to change.

| Parameter         | Value                |
|------------------:|:---------------------|
| ARMING_CHECK      | Disabled             |
| ATC_ACCEL_Y_MAX   | Disabled             |
| BRD_SAFETYENABLE  | Disabled             |
| PILOT_VELZ_MAX    | 50 cm/s              |
| PILOT_ACCEL_Z     | 50 cm/s/s            |
| ATC_RAT_YAW_FILT  | 30                   |
| THR_MIN           | 0                    |

The following are the recommended control system parameters for the BlueROV. These can be changes to make the response faster or slower and make the vehicle more or less stable.

| Parameter         | Value                |
|------------------:|:---------------------|
| ACCEL_Z_D         | 0.0                  |
| ACCEL_Z_I         | 3.0                  |
| ACCEL_Z_P         | 1.0                  |
| POS_Z_P           | 3.0                  |
| VEL_Z_P           | 8.0                  |

### Setup Voltage and Current Measurement

On the *Power* tab choose the appropriate setup. If using the standard 3DR Power Module, choose *Analog Voltage and Current*, the appropriate battery capacity, and the *Power Module 90A*.

<img src="/images/qgc/power-setup-1.png" class="img-responsive img-center" />

### Flight Mode Setup

Currently only the *Stabilize* and *AltHold* modes are used. On the *Flight Modes* tab, set all flight modes to *Stabilize* except for "Flight Mode 2", which should be set to *AltHold*. As new flight modes are added to ArduSub, these can be configured to activate those modes.

<img src="/images/qgc/flight-mode-setup-1.png" class="img-responsive img-center" />

### Camera Tilt Setup (if used)

Select the *Camera* tab. The "Gimbal Tilt" settings are used for the camera tilt. Choose whichever channel the servo is plugged into for "Output channel" and *RC8* for "Input channel". Select *Servo* for the "Type" under "Gimbal Settings" on the right.

<img src="/images/qgc/camera-tilt-setup-1.png" class="img-responsive img-center" />

Is desired, you can check the *Stabilize* box, which will enable auto-stabilization of the camera based on the vehicle pitch angle. We generally leave this unchecked.

### Lights Setup

The lights feature is currently setup to support lights that use a standard servo PWM signal for control. Until light support is officially added to QGC, the "Gimbal Roll" settings are used to connect the light input to a servo output.

Select an available channel for the "Output channel" and *RC9* for the "Input channel". Make sure that "Servo reverse" and "Stabilize" and *not* checked. Set the "Servo PWM limits" to 1100 to 1900.

<img src="/images/qgc/lights-setup-1.png" class="img-responsive img-center" />

## Configuring Motor Directions

Due to clockwise and counterclockwise propellers, as well as wiring, the motor directions will have to be tested and corrected during initial setup. *ArduSub* includes a set of parameters for this purpose. The parameters are called `MOT_1_DIRECTION` for motors 1-8 and valid values are `1` (normal) or `-1` (reverse).

We generally follow this process to check motor rotation directions:

1. Arm vehicle after completing all of the setup steps above
2. Move the "forward" joystick forward and verify that the thrusters that produce some forward thrust are operating in the correct direction
3. Move the "vertical" joystick upwards and verify that the thrusters that produce some vertical thrust are operating int the correct direction

Provided that the correct frame configuration was chosen during compilation, you should not need to perform any more validation than that.