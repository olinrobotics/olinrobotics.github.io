---
title: Pixhawk Parts
layout: template
filename: pixhawk_parts
---

# Pixhawk PX4 Documentation

###### *Last edited on 7/26/2016*

## PX4 Setup- Parts Breakdown

#### Pixhawk PX4 

> ![Pixhawk](../images/Pixhawk.png)

#### DSM X Spectrum Satellite Receiver

> ![Receiver](../images/Receiver.jpg)

#### Paired Telemetry Antennae

> ![Telem](../images/Telem.jpg)

#### PX4 Speaker

> ![Speaker](../images/Speaker.jpg)

#### 3DR’s BEC Power module

Note: Connects to POWER on PX4

> ![BEC](../images/BEC.png)

#### Motor Safety Switch

> ![Switch](../images/Switch.png)

#### Mini SD Card in Pixhawk

 > ![SD](../images/SD.png)

#### GPS module- Connects to CAN & GPS

> ![GPS](../images/GPS.png)
 
#### 4 ESC Speed controllers

Consult [Ardupilot](http://ardupilot.org/copter/docs/connect-escs-and-motors.html) for your specific type of quadcopter and plug the ESCs into your Pixhawk's MAIN OUT channels 1-4 in the correct order.

> ![ESC](../images/ESC.png)



## Minimum Requirements

This is a list of the absolute minimum number of parts you need installed to operate your vehicle safely in different modes.

#### Quadcopter

To fly in Stabilize Mode (on a copter) or drive in Manual mode (on a rover) you will need...

 - A Pixhawk with correct firmware and calibration uploaded
 - A [battery](http://images6.wheelspinmodels.co.uk/EFLB0998-a47e.jpg), typically a 3 cell (11.1 volts, 5100 milliamp-hours)
 - [BEC voltage regulator](../images/BEC.png)
 - The appropriate number of motors for your vehicle
 - The same number of [ESCs](../images/ESC.png) as motors (Quad, Hex, Octo, etc etc -Copters only)
 - A motor controller, such as a [Sabertooth](https://www.dimensionengineering.com/datasheets/Sabertooth2x12.pdf) or a [Kangaroo](https://www.dimensionengineering.com/datasheets/KangarooManual.pdf) (Ground vehicles only)
 - An RC receiver radio, preferably a [DSMX](../images/Receiver.jpg) or equivalent
 - A RC transmitter that has been [bound](link) to the RC receiver
 
To fly in Loiter or Auto Mode, or drive in Hold or Auto Mode, you will need...
- All of the above
- A [GPS](../images/GPS.png)
- A Compass (Your Pixhawk contains an internal compass.)

Use of a [Buzzer](../images/Speaker.jpg) and [Telemetry equipment](../images/Telem.jpg) is optional, but highly encouraged, as they make debugging a lot easier (and safer!)

[Click here for information on changing your Telemetry Net ID](https://olinrobotics.github.io/net_ids)

## Installing the Firmware

[Click here for instructions from Ardupilot on how to install the firmware](http://ardupilot.org/copter/docs/common-loading-firmware-onto-pixhawk.html)

## Calibrating Settings

Calibrate these before your first flight.

[Compass Calibration Instructions](http://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html)
[Radio Calibration Instructions](http://ardupilot.org/copter/docs/common-radio-control-calibration.html)
[Accelerometer Calibration Instructions](http://ardupilot.org/copter/docs/common-accelerometer-calibration.html)
[Setting your Flight Modes](flight_modes)

