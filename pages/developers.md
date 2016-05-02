---
layout: default
title: "Developers"
permalink: /developers/
nav:
- How to Get the Code: how-to-get-the-code
- Compiling: compiling
- Uploading: uploading
- Running: running
- Making a Custom Configuration: making-a-custom-configuration
- Adding Features: adding-features
---

# {{page.title}}

## How to Get the Code

The ArduSub code is maintained in a *git* repository. The best way to get the code is to clone that repository.

	git clone https://github.com/bluerobotics/ardusub.git

You can also download the code as a zip file from the right sidebar of the <a href="https://github.com/bluerobotics/ardusub.git">Github website</a>.

## Compiling

- [Mac Instructions](http://dev.ardupilot.com/wiki/building-px4-with-make-on-mac/)
- [Linux Instructions](http://dev.ardupilot.com/wiki/building-px4-for-linux-with-make/)
- [Windows Instructions](http://dev.ardupilot.com/wiki/building-px4-with-make/)

To compile the ArduSub branch, first `cd ArduSub` to enter the directory and then use a command with the following format:

	make [board type]-[frame type]

For example,

	make px4-v2-vectored

The available board types can be seen by entering `make` with no arguments. Below are the available frame types.

| Frame          | Function                                                             |
|---------------:|:-------------------------------------------------------------------- |
| `bluerov`      | Compile for BlueROV thruster configuration                           |
| `vectored`     | Compile for vectored w/ side-by-side vertical thruster configuration |
| `vectored6dof` | Compile for vectored w/ corner vertical thruster configuration       |

## Uploading

To upload the code to a PixHawk or similar controller, add `-upload` to the build command. For example:

	make px4-v2-vectored-upload

## Running

The code begins running immediately once uploaded. For Linux-based autopilots, it must be launched or started with launch script. Please see the documentation for your respective autopilot.

## Making a Custom Configuration

One of the biggest additions to the ArduSub code is a six degree-of-freedom motor library that allows a wide variety of motor configurations to be set up easily. The motors libraries for each configuration are built on a set of higher-level motor classes as follows:

    AP_Motors
        |---- AP_MotorsMulticopter
                       |---- AP_MotorsMatrix
                                    |---- AP_Motors6DOF
                                                |---- AP_MotorsBlueROV
                                                |---- AP_MotorsVectoredROV
                                                |---- AP_MotorsVectored6DOF
                                                |---- AP_Motors[New configuration]

To add a new motor configuration, you will create a new frame type and implement the `AP_Motors[New configuration]` for the new frame configuration.

## Adding Features

To be completed.