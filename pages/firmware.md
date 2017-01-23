---
layout: default
title: "Downloads"
permalink: /firmware/
nav:
- Pixhawk Firmware: firmware
- Raspberry Pi Image: images
- Parameter Files: parameter-files
---

# Firmware

Compiled firmware is now available and can be downloaded from [firmware.ardusub.com](http://firmware.ardusub.com). See here for [instructions on how to flash the Pixhawk](/initial-setup/#loading-firmware-on-pixhawk). Firmware is available for the following hardware:

#### Pixhawk (px4-v2)

**Stable Release:** <i class="fa fa-download" aria-hidden="true"></i> [ArduSub-3.4](http://firmware.ardusub.com/Sub/stable/v3.4/)

The stable release is the recommended download for most users.

**Latest Build:** <i class="fa fa-download" aria-hidden="true"></i> [ArduSub Firmware Repository](http://firmware.ardusub.com/Sub/latest)

This is the latest build of the developmental master branch. This build should only be used by developers and advanced users.

## Release History

**ArduSub-3.4** *(2016-12-30)* Download [ArduSub-3.4 here](http://firmware.ardusub.com/Sub/stable/v3.4/)

ArduSub v3.4 is the first official stable release of ArduSub. After nearly a year of steady development, testing, and improvement, ArduSub has become one of the most capable ROV control systems available.

**Important Note for ArduSub-3.4:** Many unused and inapplicable parameters that ArduSub inherited from ArduCopter have been removed. As a consequence, after upgrading to V3.4 and later, all of the parameters will be erased, and the default parameters will be loaded. **You should save your parameters before flashing this firmware.** After upgrading the firmware, you can load your saved parameter file through QGroundControl. When loading your old parameter file through QGroundControl, you will see many errors about parameters that have been removed, this is okay. After you load your parameter file, you need to change the SYSID_SW_MREV parameter to 1 before rebooting in order to prevent the default parameters from being reloaded. This procedure will only have to be done when upgrading from firmware version 3.4-dev. Subsequent releases will keep the same parameter format, so this will only have to be done once. If you are using a BlueROV2, it is recommended that you load the [Standard ArduSub Parameters](http://firmware.ardusub.com/parameters/latest/bluerov2.params) after upgrading. The upgrade process is demonstrated in the video below.

<div align="center">
	<iframe width="560" height="315" src="https://www.youtube.com/embed/siJoON6hgq4" frameborder="0" allowfullscreen></iframe>
</div>

# Images

A fully set up image for the Raspberry Pi is available here. This image is used to set up the Raspberry Pi 3 computer as a *companion computer* for the Pixhawk autopilot. See here for [instructions on how to flash the image to the SD card](/raspi-setup/#easy-setup-with-disk-image).

<i class="fa fa-download" aria-hidden="true"></i> [Latest Ardusub-Raspbian Image](http://img.ardusub.com/2017-01-12-ardusub-raspbian.img.zip) *(1.47 GB, Updated 2016-10-19)*

# Parameter Files

These files have the recommended parameters for ArduSub, making it easy to setup and update parameters on your vehicle. These parameters will not adjust your accelerometer calibration, compass calibration, or motor directions, but will change joystick button setup, PID controller values, and all other parameters.

<i class="fa fa-download" aria-hidden="true"></i> [Standard ArduSub Parameters](http://firmware.ardusub.com/parameters/latest/bluerov2.params)