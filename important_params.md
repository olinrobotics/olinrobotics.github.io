---
title: Important Parameters for the Pixhawk
layout: template
filename: important_params
--- 

# Important Parameters

###### Find a full list of parameters [here.](http://ardupilot.org/copter/docs/parameters.html)

## [ARMING_REQUIRE](http://ardupilot.org/plane/docs/arming-throttle.html)

Arming Require controls whether throttle arming is used in addition to the safety switch, and how much voltage is sent to the motors prior to throttle arming.

ARMING_REQUIRE=0: Throttle arming is disabled, meaning the safety switch is reponsible for arming and disarming the vehicle.
ARMING_REQUIRE=1: Before the user arms throttle, minimum PWM is sent to the throttle channel. This may result in the vehicle moving before being throttle armed.
ARMING_REQUIRE=2: Before the user arms throttle, no PWM signal is sent to the throttle channel. This ensures the vehicle will not move when disarmed, but may result in some ESCs beeping angrily.

## [ARMING_CHECK](http://ardupilot.org/copter/docs/parameters.html#arming-check-arming-check)

Arming check controls whether prearm safety checks are enabled, and which safety checks are performed prior to arming.

| Bit | Meaning                       |
|-----|-------------------------------|
| -1  | No safety checks enabled      |
| 0   | All safety checks enabled     |
| 1   | Barometer check enabled       |
| 2   | Compass check enabled         |
| 3   | GPS check enabled             |
| 4   | Inertial sensor check enabled |
| 5   | Check all parameters          |
| 6   | RC Control connected check    |
| 7   | Board voltage adequate check  |


*This webpage is currently under construction. Last edited on 7/28/2016.*
