---
layout: default
title: "Firmware"
permalink: /firmware/
nav:
- Firmware: firmware
- Raspberry Pi Image: images
---

# Firmware

## Overview

There are three different types of firmware:

 - Stable: The recommended build for most users.
 - Beta: A pre-release of a stable build, used for testing and bugfixes before officially labeling a build as stable. The versions for the these builds are suffixed with *-rcx*, where rc stands for release candidate, and x is a number that is incremented as the beta is updated.
 - Development: Development build, updated frequently. This build should only be used in practice by developers and advanced users. The versions for these builds are suffixed with *-dev*.

The latest stable release of ArduSub is 3.4. The current beta is 3.5-rc1, and requires a recent build of QGroundControl (later than 3.1.3) to operate. The latest development version is 3.6-dev.

## What Version is Installed?

To find out what firmware version is installed on your autopilot, [refresh your parameters](/configuring/#parameters). When the parameters are refreshed, the autopilot sends its software version information via STATUSTEXT messages. You can view these messages by clicking the *Messages* icon in QGroundControl. The *Messages* icon looks like a megaphone, or a warning sign if there are pending warnings. Here, you can see that the ArduSub version is *V3.5-rc1*.

<img src="/images/firmware/statustext-version.png" class="img-responsive img-center" style="max-height:600px;">

## Updating

It is **highly recommended** to [save your parameters](/configuring/#saving-and-loading) to a file before updating your firmware. To update your firmware, go to the *Vehicle Setup Page* and click the *Firmware* tab. Plug your autopilot into the computer with a USB cable. Click ArduPilot flight stack, and choose your desired version to load. Beta and Development options are available after clicking the *Advanced settings* checkbox. *Stable* is not yet available through QGC for ArduSub. After you have selected your desired version, click *Ok* and wait for the upload to complete.

<img src="/images/firmware/qgc-upgrade.png" class="img-responsive img-center" style="max-height:600px;">

## Firmware Files

Compiled firmware is now available and can be downloaded from [firmware.ardusub.com](http://firmware.ardusub.com). See here for [instructions on how to flash the Pixhawk](/initial-setup/#loading-firmware-on-pixhawk). Firmware is available for the following hardware:

#### Pixhawk (px4-v2)

**Stable Release:** <i class="fa fa-download" aria-hidden="true"></i> [ArduSub-3.4](http://firmware.ardusub.com/Sub/stable/v3.4/)

The stable release is the recommended download for most users.

**Latest Build:** <i class="fa fa-download" aria-hidden="true"></i> [ArduSub Firmware Repository](http://firmware.us.ardupilot.org/Sub/latest/PX4/ArduSub-v2.px4)

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

<i class="fa fa-download" aria-hidden="true"></i> [Latest Ardusub-Raspbian Image](http://img.ardusub.com/2017-01-12-ardusub-raspbian.img.zip) *(1.6 GB, Updated 2017-01-12)*

