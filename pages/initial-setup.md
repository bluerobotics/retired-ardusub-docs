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
- Configuring Joystick/Gamepad: configuring-joystickgamepad
- Configuring Parameters: configuring-parameters
- Configuring Motor Directions: configuring-motor-directions
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

If using an Ethernet connection with companion computer, you must must connect to the autopilot via `mavproxy`. This setup will work with a variety of configurations including:

- PixHawk Connected to Raspberry Pi via USB or serial

#### Raspberry Pi Initial Setup

We first need to configure the Raspberry Pi to connect directly over Ethernet without a router. This will require setting a static IP address so we can reliably connect to the Raspberry Pi. You can do this by adding the following to the end of the line in `/boot/cmdline.txt`.

```
ip=169.254.2.2
```

You should also set up your computer to have a static IP address when connected to the Ethernet connection. We recommend using the address 169.254.2.1.

Next you'll need to get the companion computer scripts. Make sure you have an internet connection to the Raspberry Pi and enter the following:

```
sudo apt-get update
sudo apt-get install gstreamer1.0
git clone https://github.com/bluerobotics/companion.git
```

Next, we'll set up the companion computer scripts to run automatically at boot. Enter the following commands to do so:

```
cd companion/RPI2/Raspbian
sudo ./rov-setup.sh
```

### Ethernet Connection with Linux Autopilot (Navio, BBBmini, etc.)

For Linux based autopilots, the network connection is launched when the ArduSub code is started. For examples, please see the documentation for your respective autopilot.

## Calibration

Once the controller is connected to QGC for the first time, we must calibrate the accelerometers, compass, and joystick.

1. Go to the settings tab in QGC and select the red *Sensors* tab on the left sidebar.
2. Choose your autopilot orientation (none for the BlueROV).
3. Click on *Accelerometers* and follow the instructions.
4. Click on *Compass* and follow the instructions.
5. When completed, the *Sensors* tab will no longer be red.

## Configuring Joystick/Gamepad

*ArduSub* provides a number of parameters to map controller buttons to various functions. This setup is required as there are no defaults configured.

Each button can be assigned to one primary function and one alternate "shift" function. If the "shift" functions are used, then a "shift" button must be assigned. This works like the shift key on your keyboard, altering the functionality of other buttons while pressed.

In the parameters, you will find a number of parameters named `BTN1_FUNCTION` (normal function) and `BTN1_SFUNCTION` (shift function) for each button. You can find the button numbers on the "joystick" tab in QGroundControl.

The following is a list of functions that can be assigned to buttons:

| Function                    | Assignment Value     |
|----------------------------:|:---------------------|
| None                        | 0                    |
| Shift                       | 1                    |
| Arm Toggle                  | 2                    |
| Arm                         | 3                    |
| Disarm                      | 4                    |
| Mode Toggle                 | 5                    |
| Enter Flight Mode 1         | 6                    |
| Enter Flight Mode 2         | 7                    |
| Enter Flight Mode 3         | 8                    |
| Enter Flight Mode 4         | 9                    |
| Enter Flight Mode 5         | 10                   |
| Enter Flight Mode 6         | 11                   |
| Camera Mount Tilt to Center | 21                   |
| Camera Mount Tilt Up        | 22                   |
| Camera Mount Tilt Down      | 23                   |
| Camera Shutter Trigger      | 24                   |
| Lights 1 Cycle Brightness   | 31                   |
| Lights 1 Increase Brightness| 32                   |
| Lights 1 Decrease Brightness| 33                   |
| Lights 2 Cycle Brightness   | 34                   |
| Lights 2 Increase Brightness| 35                   |
| Lights 2 Decrease Brightness| 36                   |
| Gain Toggle                 | 41                   |
| Gain Increase               | 42                   |
| Gain Decrease               | 43                   |
| Trim roll right             | 44                   |
| Trim roll left              | 45                   |
| Trim pitch up               | 46                   |
| Trim pitch down             | 47                   |

## Configuring Parameters

A number of parameters should be adjusted at startup for use with ArduSub. The following table shows the currently recommmended parameters to change.

| Parameter         | Value                |
|------------------:|:---------------------|
| ARMING_CHECK      | Disabled             |
| ATC_ACCEL_Y_MAX   | Disabled             |
| BRD_SAFETYENABLE  | Disabled             |
| FS_CRASH_CHECK    | Disabled             |
| DISARM_DELAY      | 0                    |
| EK_ALT_NOISE      | 0.1                  |
| GND_PRIMARY       | 2ndBaro              |
| PILOT_VELZ_MAX    | 50 cm/s              |
| PILOT_ACCEL_Z     | 50 cm/s/s            |
| POS_Z_P           | 8.0 (above limit)    |
| RATE_YAW_FILT_HZ  | 30                   |
| THR_MIN           | 0                    |

Please confirm that the following settings are set this way. These should be set by default but can be different on some platforms.

| Parameter         | Value                |
|------------------:|:---------------------|
| RCMAP_PITCH       | 1                    |
| RCMAP_ROLL        | 2                    |
| RCMAP_THROTTLE    | 3                    |
| RCMAP_YAW         | 4                    |
| RCMAP_FORWARD*    | 6                    |
| RCMAP_STRAFE*     | 7                    |

*<small>These are shown in the "default group" panel.

The following are the recommended control system parameters for the BlueROV. These can be changes to make the response faster or slower and make the vehicle more or less stable.

| Parameter         | Value                |
|------------------:|:---------------------|
| ACCEL_Z_D         | 0.0                  |
| ACCEL_Z_I         | 3.0                  |
| ACCEL_Z_IMAX      | 1000.0               |
| ACCEL_Z_P         | 1.0                  |
| PILOT_ACCEL_Z     | 50.0                 |
| POS_Z_P           | 3.0                  |
| STB_PIT_P         | 12.0                 |
| STB_RLL_P         | 12.0                 |
| STB_YAW_P         | 12.0                 |
| VEL_Z_P           | 8.0                  |

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

## Configuring Motor Directions

Due to clockwise and counterclockwise propellers, as well as wiring, the motor directions will have to be tested and corrected during initial setup. *ArduSub* includes a set of parameters for this purpose. The parameters are called `MOT_MOT1_REVERSE` for motors 1-8 and valid values are `1` (normal) or `-1` (reverse).

We generally follow this process to check motor rotation directions:

1. Arm vehicle after completing all of the setup steps above
2. Move the "forward" joystick forward and verify that the thrusters that produce some forward thrust are operating in the correct direction
3. Move the "vertical" joystick upwards and verify that the thrusters that produce some vertical thrust are operating int the correct direction

Provided that the correct frame configuration was chosen during compilation, you should not need to perform any more validation than that.