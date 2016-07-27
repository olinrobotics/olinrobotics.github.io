---
title: Odroid
layout: template
filename: odroid_info
---

# Odroid and Inter Computer Communication Documentation

## Contents
- [Odroid Setup](#odroid-setup)
- [Using the Odroid](#using-the-odroid)
- [Odroid and ROS](#odroid-and-ros)
- [Using GPIO pins](#using-gpio-pins-on-the-odroid)
- [PWM on odroid](#pwm-on-the-odroid)
- [Setup Wifi Dongle](#setting-up-wifi-on-the-odroid-with-a-usb-dongle)

## Useful Links
- [flashing os images to sd cards](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md)
- [ARM ros install](http://wiki.ros.org/indigo/Installation/UbuntuARM)
- [ROS setup shell scripts repository](https://github.com/olinrobotics/Odroid_Setup)

## Odroid Setup
There were a couple of places we had to go to setup the Odroid:

- We used the most recent image [from here](http://east.us.odroid.in/ubuntu_14.04lts/) and have tested both the minimal and lubuntu images.
- Download the image you want and extract it using: `xz -d <image_file.xz>`
  - note: I like to move the image file to another directory so I know where it is before I extract it.
- We followed [these raspberry pi instructions](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md) to flash the SD card with the image. Just use the odroid image you downloaded in place of the raspian image in the instructions.
  - [these odroid instructions](http://odroid.us/mediawiki/index.php?title=Step-by-step_Ubuntu_SD_Card_Setup) specifically reference the odroid, but they have some commands that weren't working and are generally less clear.
  - If you are having problems, make sure the card has the label you think it has. Every time I have flashed an SD card, it has been in `/dev/sdx` (where x is whatever the next letter is after your hard drives)
- After following these instructions, we had to edit the `boot.ini` file to set the resolution of the connected display before we could see the image (instructions for editing the file are in comments in the file)
- After flashing the SD card, insert it in the Odroid and power it up.  If everything worked correctly, both the red power light and the blue status light will light up within a few seconds.

## Using the Odroid
There are multiple methods of getting an odroid to run the code you want it to run, and they should be chosen based on your application. (note, all of these strategies work on Raspberry Pis and other single board computers as well)

### Use the Odroid like a desktop:
Plug in a mouse, keyboard, and monitor, power up the Odroid, and use it like a normal computer.

This works perfectly well, and is usually how you test if flashing the sd card worked correctly.  You can do anything you want with it in this configuration, but it requires a lot of hardware and is therefore impractical for when the odroid is on a vehicle.

### Use SSH:
ssh is a method of opening a terminal on another computer.  It is built in for linux and mac, and can be used with a bit of messing around in Windows. This method is extremely useful because it allows you to do anything you can do from a terminal window on the odroid with only an internet connection between the two computers.

#### Find IP address
In order to ssh into the odroid, you need to know its IP address. You can do this by connecting the odroid to a network, then connecting to that network yourself, finding its IP address, and connecting, but the simpler method is to connect the odroid directly to your computer with an ethernet cable.  You then need to setup an ethernet connection on your computer to share internet to other computers (from linux):
- click on the wifi symbol in the top right
- select edit connections
- click add, then select ethernet connection
- go to `IPv4 Settings` and select `Shared to other computers` from the drop down menu
- save the connection
Now, connect an ethernet chord between your computer and the odroid, and select your new network.  Use `ifconfig` to find your IP address on the new network (should end with .0.1), then use `nmap ##.##.##.0/24` with the first three sections of the IP address you just found to find all IP address on that network.

#### SSH in
Once you know the odroid's IP address, run `ssh <username>@<ipaddress>`

By default, the username is **root** and the password is **odroid**.

You should be prompted for the odroid's password, then you should get the command prompt of the odroid.

Congratulations, you now have a terminal which is actually running commands on a different computer.

### Directly edit the SD card
The odroid stores its entire file system on an SD card. This means that you can take that SD card out of the Odroid, plug it into your computer, and edit any files you want.  You use this method to set the resolution of the monitor in the boot.ini file before the first boot up.  It is also useful for getting files onto the Odroid, and can even be the primary method of interacting with the Odroid, especially if it is set up to run your code on startup.

## Odroid and ROS
We used [these instructions](http://wiki.ros.org/indigo/Installation/UbuntuARM) to install ROS on the ODROID.  They worked fine, so you should be able to just follow them.

Once ROS is installed, you can run roscore as well as any programs which use ROS, but more setup is needed to be able to communicate with a roscore on the odroid from another computer.  We set up a [github repository](https://github.com/olinrobotics/Odroid_Setup) with some shell scripts to automatically setup the odroid to communicate with other computers.  These scripts set the `ROS_MASTER_URI` and `ROS_IP` variables to point at the correct IP address so that other computers can see the roscore running on the odroid.  Instructions for using these scripts are in that repository's README.

## Using GPIO Pins on the ODROID

![pinout](images/odroid_pins.png)

### CLI

```bash
echo ${PIN} > /sys/class/gpio/export # PIN = whichever GPIO pin you decided to use
echo ${MODE} > /sys/class/gpio/gpio${PIN}/direction # MODE = 'in' or 'out'  
echo ${VALUE} > /sys/class/gpio/gpio${PIN}/value # VALUE = 1 for HIGH and 0 for LOW
echo ${PIN} > /sys/class/gpio/unexport # Done with using PIN
```

###  C/C++

See [This Github Repo](https://github.com/yycho0108/GPIO_Interface) for Basic C++ interface with GPIO.

For more sophisticated applications, see [This Github Repo](https://github.com/hardkernel/wiringPi).

Currently, software PWM on wiringPi doesn't work on the ODROID C1/C1+.


## PWM ON THE ODROID

ODROID HAS 2 Hardware PWM output pins, 33 and 19.

To use the PWM output module, follow the instructions below:

```bash
# START PWM MODULE IN KERNEL
sudo modprobe pwm-meson npwm=1 #USING 1 PWM PIN (33)

# ALTERNATIVELY, TO USE BOTH 33 and 19, run:
#sudo modprobe pwm-meson npwm=2 #USING 1 PWM PIN (33, 19)

# START PWM CONTROL
sudo modprobe pwm-ctrl

# CHANGE DIRECTORY
cd /sys/devices/platform/pwm-ctrl

# CONVENIENT ALIAS; NOT NECESSARY TO EXPORT.
# ALTERNATIVELY, WRITE VALUES DIRECTLY INSTEAD OF DEREFERENCING VARIABLE.
export DUTY_CYCLE=102 # 0 ~ 1023
export FREQUENCY=1024 # IN Hz, 0 ~ 1000000

# SET DUTY CYCLE
echo ${DUTY_CYCLE} > duty0

# ENABLE PWM
echo 1 > enable0

# SET FREQUENCY
echo ${FREQUENCY} > freq0

# WHEN YOU'RE DONE, REMOVE MODULES FROM KERNEL
sudo modprobe -r pwm-ctrl
sudo modprobe -r pwm-meson
```

## Setting Up WiFi on the ODROID with a USB Dongle

```bash
# FOLLOW THE STEPS SEQUENTIALLY, EXCEPT [TIP]S
# INSTALL THE TOOLS
	sudo apt-get install wireless-tools wpasupplicant

# [TIP] STATUS-CHECKING
	dmesg | tail # CHECKS GENERAL DEVICE STATUS (AND OUTPUT THE END OF IT)
	iwconfig # CHECKS WIRELESS DEVICE STATUS
	ifconfig # CHECKS GENERAL NETWORK STATUS

# SCAN FOR AVAILABLE NETWORKS (CHECK THAT DEVICE FUNCTIONS PROPERLY)
	sudo iwlist wlan0 scan

# CONFIGURE NETWORK INTERFACES
	sudo -s #BECOME ROOT
	echo -e "\nauto wlan0 \niface wlan0 inet dhcp \n\twpa-ssid OLIN-ROBOTICS\n\twpa-psk R0B0TS-RULE" >> /etc/network/interfaces

# CONFIGURE WPA FOR YOUR NETWORK
	wpa_passphrase  OLIN-ROBOTICS >> /etc/wpa_supplicant/wpa_supplicant_OLIN-ROBOTICS.conf 

# START WPA_SUPPLICANT (TRY TO CONNECT TO NETWORK WITH GIVEN CONFIGURATION)
	sudo wpa_supplicant -B -D wext -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant_OLIN-ROBOTICS.conf 
	ip link show wlan0 | grep UP

# ALTERNATIVELY, START WPA_SUPPLICANT WITH LOG
	sudo wpa_supplicant -B -D wext -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant_OLIN-ROBOTICS.conf  -f /var/log/wpa_supplicant.log
	cat /var/log/wpa_supplicant.log 

# REBOOT ODROID
	sudo reboot

# ESTABLISH COMMUNICATION WITH ROUTER
	sudo dhclient -v -r wlan0

# RESTART wlan0
	sudo ifconfig wlan0 down && sudo ifconfig wlan0 up

# [TIP] IF YOU MESSED UP AND HAVE MULTIPLE PROCESSES RUNNING WPA_SUPPLICANT, GET RID OF THEM
	ps -ef | grep  "wpa_"
	sudo kill $(pgrep -f "wpa_supplicant -B")

# CHECK SUBNET CONNECTIVITY
	ping 192.168.16.73

# CHECK EXTERNAL NETWORK CONNECTIVITY (DISABLE NETWORK SHARING VIA ETHERNET CABLE IF YOU HAVE IT SET UP)
	ping www.google.com

# IF YOU'RE HERE, THEN YOU SHOULD BE ALL SET UP
```
