---
title: Odroid
layout: template
filename: odroid_info
---

# Odroid and Inter Computer Communication Documentation

## Odroid Setup
There were a couple of places we had to go to setup the Odroid:
- We used the most recent image [from here](http://east.us.odroid.in/ubuntu_14.04lts/) and have tested both the minimal and lubuntu images.
- We followed [these instructions](http://odroid.us/mediawiki/index.php?title=Step-by-step_Ubuntu_SD_Card_Setup) to flash the SD card with the image.
- After following these instructions, we had to edit the `boot.ini` file to set the resolution of the connected display before we could see the image (instructions for editing the file are in comments in the file)

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

You should be prompted for the odroid's password, then you should get the command prompt of the odroid.

Congratulations, you now have a terminal which is actually running commands on a different computer.

### Directly edit the SD card
The odroid stores its entire file system on an SD card. This means that you can take that SD card out of the Odroid, plug it into your computer, and edit any files you want.  You use this method to set the resolution of the monitor in the boot.ini file before the first boot up.  It is also useful for getting files onto the Odroid, and can even be the primary method of interacting with the Odroid, especially if it is set up to run your code on startup.
