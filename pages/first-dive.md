---
layout: default
title: "First Dive"
permalink: /first-dive/
nav:
- Joystick/Controller Functions: joystick-controller-functions
- Dive Modes: dive-modes
- Arming and Disarming: arming-and-disarming
- Tuning: tuning
- Pre-Dive Checklist: pre-dive-checklist
- Launching Video Stream: launching-video-stream
- Recording Video: recording-video
---

# {{page.title}}

This section covers the information you will need to know for your first dive and also some basic configuration to get your ROV diving well.  

## Joystick/Controller Functions

The gamepad controls the ROV during operation. It has been tested with the Microsoft Xbox controller and the Logitech F310. The following joysticks and buttons are used:

- **Left Stick:** Forward and strafe input
- **Right Stick:** Throttle and yaw input
- **Start Button:** Arm vehicle
- **Back Button:** Disarm vehicle
- **Y Button:** Switch to althold (learning) mode
- **B Button:** Switch to stabilize (manual) mode
- **Right Bumper:** Increase light brightness
- **Left Bumper:** Decrease light brightness
- **Buttonpad Up/Down Arrows:** Tilt camera (if applicable and set up in QGC)
- **Buttonpad Left/Right Arrows:** Increase/decrease roll trim (if IMU is not completely level)
- **Left Joystick Click:** Reset camera tilt angle

## Dive Modes

**Stabilize Mode**, shown in QGC as **Manual Mode**, is the default mode of operation. The vehicle automatically stabilizes to level roll and pitch angle and maintains heading when not commanded to turn. The throttle control is left entirely to the pilot.

**AltHold Mode**, shown in QGC as **Learning Mode**, is the same as stabilize mode with the addition of automatic depth holding. The throttle control is used to increase or decrease the holding depth.

## Arming and Disarming

By default, the vehicle is disarmed and the motor outputs are disabled. The camera servo and lights will still function when disarmed. 

When armed, the vehicle will actively try to stabilize and the pilot control inputs will be output to the thrusters.

## Tuning

There are a number of control system tuning parameters that can be adjusted to change the performance of the system. Please see the ArduCopter documentation for a detailed description of these parameters.

## Pre-Dive Checklist

To be completed.

## Launching Video Stream

The following command shows how to start a video stream from the Raspberry Pi that can be automatically displayed in the QGroundControl display.

```
raspivid -n -fl -w 1280 -h 720 -b 10000000 -fps 30 -t 0 -o - | gst-launch-1.0 -v fdsrc ! h264parse ! rtph264pay config-interval=10 pt=96 ! udpsink host=<remote ip> port=5600
```

The following will stream video at 30 fps and 1080p resolution, typically with latency of around 300ms.

```
raspivid -n -md 2 -b 25000000 -fps 30 -t 0 -awb off -o - | gst-launch-1.0 -v fdsrc ! h264parse ! rtph264pay config-interval=10 pt=96 ! udpsink host=<remote ip> port=5600 
```

## Recording Video

On Mac we recommend using Quicktime to record the entire screen during operation. This will save the telemetry data that is displayed on the screen as well.
