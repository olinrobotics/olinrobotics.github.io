---
title: Telemetry Net IDs
layout: template
filename: net_ids
---

# Net IDs

## What is a Telemetry Net ID?

A Telemetry Net ID is the ID your telemetry radios use to ensure they are communicating with eachother and not other vehicles. 
25 is the default number set by Mission Planner, and as such, has a high chance of getting or sending communications from the wrong vehicle.
This can be disastrous in Auto mode, as vehicles may move unpredictably.

## Find Your Net ID

This is a omprehensive list of all Telemetry Net IDs currently in use by the Olin Intelligent Vehicles Lab, and which projects they are assigned to.
25 is the default number set by Mission Planner.

- 103:
- 104:
- 154:
- 254:
- 42: Lavabot (spare)
- 40: Lavabot

## How to Set your Telemetry Net ID

1. Connect your vehicle to battery power and turn it on. 
2. Connect your ground control Telemetry unit to your computer via a miniUSB to USB cable.
3. Do not connect via telemetry to Mission Planner. Disconnect if you have already connected.
4. Under the "Initial Setup" tab, click the "Optional Hardware" menu, then "Sik Radio."
5. Click the "Load Settings" button at the top of the Sik Radio page.
6. Change your current settings as necessary, then click the "Save Settings" button.

[Click here for more detailed instructions from Ardupilot](http://ardupilot.org/copter/docs/common-configuring-a-telemetry-radio-using-mission-planner.html)

*This Github page is currently under construction.*
