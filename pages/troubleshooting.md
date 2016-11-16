---
layout: default
title: "Troubleshooting"
permalink: /troubleshooting/
nav:
- Troubleshooting: troubleshooting
- Logging: logging
---

# {{page.title}}

This page shares issues that users have run into and how they were resolved. Hopefully this will help to solves issues for others.

## Vehicle Control

**Vehicle turns or moves even when not controlled to do so.**

Please check RCx_TRIM parameters to make sure that all trims are set to 1500.

**Motors spin fast as soon as the vehicle is armed.**

First, check to make sure that the joystick throttle is set to "Full down is zero throttle". If that does not fix it, check that the vehicle is calibrated level properly.

## Logging
There are two types of logs that can be used to diagnose problems while running ArduSub, or to retrieve data for post-processing.

**Telemetry logs**

Telemetry logs store recieved MAVLink messages. MAVProxy and QGroundControl save telemetry logs locally in a **.tlog** file. Telemetry logs are the preferred way of diagnosing most problems.

Once connected to the autopilot, MAVProxy will save all telemetry to a file called 'mav.tlog'. The mav.tlog file is saved under the same path from which MAVProxy was run. By default, QGroundControl only begins logging telemetry after the vehicle has been armed. QGroundControl can be configured to log telemetry while the autopilot is disarmed by clicking the 'Q' icon in the menu bar, then selecting the 'General' tab. Select the option to save logs 'even if vehicle was not armed' in order to log telemetry while disarmed. In order to save a telemetry log from QGroundControl, you *MUST* click save when prompted after disconnecting from the vehicle, or after quitting the application.

<img src="/images/log-disarmed-qgc.png" class="img-responsive img-center" style="max-height:400px;">
<br><br>
**DataFlash logs**

DataFlash logs are saved by the Autopilot directly to onboard memory (SD card in the case of the Pixhawk), regardless of a telemetry connection. These logs are saved in a **.bin** file. DataFlash logs are capable of logging data at a much faster rate than telemetry logs, but the file needs to be converted using MissionPlanner before it can be viewed by QGroundControl, MissionPlanner, or APMPlanner.

By default, a new DataFlash log is created when the autopilot is armed for the first time after booting. The DataFlash log will continue until the autopilot is powered down. The LOG_DISARMED parameter can be set to 'Enabled' in order to begin a DataFlash log as soon as the autopilot is booted, even before arming.

<img src="/images/log-disarmed.png" class="img-responsive img-center" style="max-height:400px;">

DataFlash logs can be retrieved in two ways:

1. Remove the Micro SD card from the Pixhawk and plug it into your computer to view and transfer the logs using a file explorer like a regular USB drive.

2. Download the logs remotely via QGroundControl or MAVProxy.

	- Log downloading via QGroundControl

		Click the 'Widgets' icon in the top menu bar, and click the 'Log Download' option.

		<img src="/images/log-download.png" class="img-responsive img-center" style="max-height:400px;">

		Click the 'Refresh' button to view available logs.

		Select the log you would like to download, and click 'Download'.

		Multiple logs can be downloaded by highlighting the desired logs before clicking 'Download'.

		<img src="/images/log-download-1.png" class="img-responsive img-center" style="max-height:400px;">

	- Log downloading via MAVProxy

		While connected to the autopilot via MAVProxy, type 'log list' in the MAVProxy console to list the available DataFlash logs onboard the autopilot.

		Type 'log download X' to download log number X

		While the log is downloading, you can type 'log status' to view the status of the download, or 'log cancel' to cancel the download.


