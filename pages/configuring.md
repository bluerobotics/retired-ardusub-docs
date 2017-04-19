---
layout: default
title: "Configuring"
permalink: /configuring/
nav:
- Parameters: parameters
---

# Parameters

## Overview

Parameters are the user configurable settings for the autopilot. They are stored on internal memory on the autopilot, and are loaded when the autopilot boots up. Some parameters require a reboot to take effect, but most do not.

## Saving and Loading

The entire set of parameters on the autopilot can be saved to a text file. Parameters can also be loaded from a text file, overwriting the current parameters on the autopilot.

To save or load parameters using QGroundControl, go to the *Vehicle Setup Page*, and click the *Parameters* tab. Click the *Tools* dropdown menu in the upper right hand corner and select *Save to file* or *Load from file*.

<img src="/images/configuring/save-parameters.png" class="img-responsive img-center" style="max-height:600px;">

## Refreshing

Some of the parameters are dynamic and will change under certain circumstances or after different events. In order to reload the current parameter values on the autopilot click *Refresh*.

## Resetting

The entire set of parameters can be erased and reset to the default values that are configured in the autopilot firmware by clicking *Reset all to defaults* (ArduSub V3.5+ only).

