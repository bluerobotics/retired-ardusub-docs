---
layout: default
title: "Troubleshooting"
permalink: /troubleshooting/
nav:
- Troubleshooting: troubleshooting
- Logging: logging
- Issue Reporting: issue-reporting
---

# {{page.title}}

This page shares issues that users have run into and how they were resolved. Hopefully this will help to solves issues for others.

## Vehicle Control

**Vehicle flips itself over**

Check that the motor directions are [configured correctly](/initial-setup/#configuring-motor-directions). Also check that the motors are connected to the correct motor outputs on the flight controller, according to the [supported frame diagrams](/introduction/#supported-frames).

**Vehicle turns or moves even when not controlled to do so.**

Please check RCx_TRIM parameters to make sure that all trims are set to 1500, with the exception of RC3_TRIM, which should be set to 1100.

**Motors spin as soon as the vehicle is armed.**

First, check to make sure that the joystick throttle is set to "Full down is zero throttle". If that does not fix it, check that the vehicle is calibrated level properly, and that the vehicle is sitting level.

The flight controller attempts to stabilize the vehicle's attitude so that it is perfectly level. If the vehicle's attitude is off from level, even a fraction of a degree, the flight controller will spin the motors in an attempt to correct the error. If the vehicle is sitting on land, the error will not change, and the flight controller will spin the motors faster and faster as it tries harder and harder to correct the error. Testing the vehicle on land should be done in MANUAL mode, which just passes pilot inputs to the motors with no stabilization.

## No Telemetry (No Pixhawk Connection)

Check that the Pixhawk is plugged into the companion computer (Raspberry Pi) via USB. Make sure that you are using a USB cable with data lines, some USB cables only provide power and will not allow communication. You can connect the Pixhawk to the surface computer directly with the USB cable to verify that the USB cable works.

Check your network settings. The surface computer should have a static IP address of 192.168.2.1. You may have to adjust your firewall settings to allow QGrouncControl access to the network. You should be able to ping the companion computer from the surface computer. On the surface computer's command line enter:

	ping 192.168.2.2

## No Video

If you do not have telemetry, please troubleshoot that first according to the above instructions.

If you have telemetry, but no video, make sure the video settings are correct in QGroundControl. The video settings are found in the General tab of the Application Settings (Q icon) view. The video source should be set to UDP video, and the port should be 5600. These are the default settings.

<img src="/images/qgc-video-settings.png" class="img-responsive img-center" style="max-height:400px;">

If the video settings are correct, and there is no video stream, the most likely cause is a faulty physical connection with the camera ribbon cable. Disconnect power to the ROV/Raspberry Pi and reseat the ribbon cable on both ends, ensuring that the contact side of the cable is oriented correctly. The contacts should face towards the board on the camera module, and towards the HDMI connector on the Raspberry Pi.

If you have checked all of the above and still don't have a video stream, you can check the video streaming process for errors. Log into the Raspberry Pi via SSH or PuTTY and enter the following command into the Raspberry Pi command line:

	sudo screen -r video

If the camera is working and the video stream is running, the output should end in something like this:

	Pipeline is PREROLLED ...
	Setting pipeline to PLAYING ...
	New clock: GstSystemClock

To return to the command line and keep the streaming process running, hit control+a then type 'd' (to detach).

If the video stream isn't running the output of the `screen` command will be:

	There is no screen to be resumed matching video.

You can relaunch the video streaming process by entering:

	~/companion/RPI2/Raspbian/start_video.sh

If the output of this command contains something like this:

	mmal: Failed to create camera component

Then the camera isn't working. Double check the camera ribbon cable, and try running `sudo rpi-update`.

## Miscellaneous

**Camera does not tilt**

The output servo rail on the Pixhawk requires a separate 5V power supply. The power module and USB power inputs on the Pixhawk will not power the servo rail. Make sure you have a 5V input on the servo rail via an ESC BEC or standalone BEC.

Check that input/output channels are [configured for camera tilt](/initial-setup/#camera-tilt-setup-if-used).

Check that joystick buttons [have been assigned](/initial-setup/#button-setup) to camera tilt functions.

**"No io thread heartbeat" message constantly appears.**

This message indicates that the APM io thread has stopped running. The most likely cause is a corrupted filesystem on the micro SD card. Remove the card from the pixhawk, and format it as FAT32. If the error persists, you will need to replace the SD card, or disable dataflash log files by setting the LOG_BACKEND_TYPE parameter to None (0).

## Logging
There are two types of logs that can be used to diagnose problems while running ArduSub, or to retrieve data for post-processing.

**Telemetry logs**

Telemetry logs store recieved MAVLink messages. MAVProxy and QGroundControl save telemetry logs locally in a **.tlog** file. Telemetry logs are the preferred way of diagnosing most problems.

Once connected to the autopilot, MAVProxy will save all telemetry to a file called 'mav.tlog'. The mav.tlog file is saved under the same path from which MAVProxy was run. By default, QGroundControl only begins logging telemetry after the vehicle has been armed. QGroundControl can be configured to log telemetry while the autopilot is disarmed by clicking the 'Q' icon in the menu bar, then selecting the 'General' tab. Select the option to save logs 'even if vehicle was not armed' in order to log telemetry while disarmed. In order to save a telemetry log from QGroundControl, you *MUST* click save when prompted after disconnecting from the vehicle, or after quitting the application.

<img src="/images/log-disarmed-qgc.png" class="img-responsive img-center" style="max-height:400px;">
<br><br>
**DataFlash logs**

DataFlash logs are saved by the Autopilot directly to onboard memory (SD card in the case of the Pixhawk), regardless of a telemetry connection. These logs are saved in a **.bin** file. DataFlash logs are capable of logging data at a much faster rate than telemetry logs. DataFlash log files can be opened and inspected with MAVProxy, APM Planner 2 or Mission Planner.

By default, a new DataFlash log is created when the autopilot is armed for the first time after booting. The DataFlash log will continue until the autopilot is powered down. The LOG_DISARMED parameter can be set to 'Enabled' in order to begin a DataFlash log as soon as the autopilot is booted, even before arming.

<img src="/images/log-disarmed.png" class="img-responsive img-center" style="max-height:400px;">

DataFlash logs can be retrieved in two ways:

1. Remove the Micro SD card from the Pixhawk and plug it into your computer to view and transfer the logs using a file explorer like a regular USB drive.

2. Download the logs remotely via QGroundControl or MAVProxy.

	- Log downloading via QGroundControl

		Click the Analyze icon at the top of the window. The icon looks like a magnifying glass over a document.

		Click the 'Refresh' button to view available logs.

		Select the log you would like to download, and click 'Download'.

		Multiple logs can be downloaded by highlighting the desired logs before clicking 'Download'.

		<img src="/images/log-download.png" class="img-responsive img-center" style="max-height:400px;">

	- Log downloading via MAVProxy

		While connected to the autopilot via MAVProxy, type 'log list' in the MAVProxy console to list the available DataFlash logs onboard the autopilot.

		Type 'log download X' to download log number X

		While the log is downloading, you can type 'log status' to view the status of the download, or 'log cancel' to cancel the download.

# Issue Reporting

We're always trying to make our documentation, instructions, software, and user experience better. If you're having an issue with anything, please report it so that we can address it as soon as possible! Here's where to do that depending on what's wrong:

- **ArduSub Issues:** For anything related to the ArduSub software that runs on the Pixhawk and controls the ROV, reports issues on the [ArduSub Github Issues Page](https://github.com/bluerobotics/ardusub/issues). If you're unsure where your issue should be posted, you can report it here.
- **QGroundControl Issues:** For anything related to the QGroundControl software, joystick setup, video streaming, etc., please report an issue on the [QGroundControl Github Issues Page](https://github.com/mavlink/qgroundcontrol/issues).
- **Documentation:** For anything related to the documentation and instructions here, please report an issue on the [ArduSub Documentation Github Issues Page](https://github.com/bluerobotics/ardusub-docs/issues).


